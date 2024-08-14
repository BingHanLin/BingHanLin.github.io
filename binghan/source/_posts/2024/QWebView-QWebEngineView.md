---
title: QWebView-QWebEngineView
tags:
    - Uncategorized
date: 2024-08-10 20:19:00
---

# Integrating Interactive Web Visualizations in C++ Applications with QWebEngineView

## Introduction

Modern application development often requires the integration of rich, interactive data visualizations to enhance user experience. This article explores how to leverage `QWebEngineView` in a C++ application to display interactive Plotly charts, demonstrating a powerful way to combine web technologies with Qt applications.

## QWebEngineView: A Brief Overview

`QWebEngineView`, part of the [Qt WebEngine Widgets module](https://doc.qt.io/qt-5/qtwebenginewidgets-module.html), is a widget for rendering web content using the Chromium browser engine. Introduced in Qt 5.4 as a replacement for `QWebView`, it offers several key features:

-   Modern web standards support (HTML5, CSS3, JavaScript)
-   Seamless C++ and JavaScript integration via Web Channel
-   Extensive JavaScript support and interaction
-   Customizable browser behavior and appearance

## Project Setup

To get started, let’s take a look at the project structure and configuration. Below is the tree structure of the project:

```
├── CMakeLists.txt
├── src/
│   ├── dataModel.hpp
│   ├── main.cpp
│   ├── mainWindow.cpp
│   ├── mainWindow.hpp
│   ├── resource/
│       ├── chart.html
│       ├── plotly.js
│       ├── resource.qrc
```

The CMakeLists.txt file provided in the project contains the necessary configuration for building the application. Below is a brief look at the essential parts of this setup:

```cmake
cmake_minimum_required(VERSION 3.15)

project(QWebEngineViewDemo)

set(CMAKE_CXX_STANDARD 17)

find_package(Qt5 REQUIRED COMPONENTS Widgets WebEngineWidgets)

qt5_add_resources(GUI_RESOURCES "${PROJECT_SOURCE_DIR}/src/resource/resource.qrc")

add_executable(${PROJECT_NAME}
    "${PROJECT_SOURCE_DIR}/src/main.cpp"
    "${PROJECT_SOURCE_DIR}/src/mainwindow.cpp"
    "${PROJECT_SOURCE_DIR}/src/dataModel.hpp"
    ${GUI_RESOURCES}
)

target_include_directories(${PROJECT_NAME} PRIVATE "${PROJECT_SOURCE_DIR}/src")

target_link_libraries(${PROJECT_NAME} PRIVATE Qt5::Widgets Qt5::WebEngineWidgets)
```

This CMake configuration ensures that the application is properly linked with the necessary Qt components, particularly Qt5::WebEngineWidgets, and is built with all required resources included.

## Initialize QtWebEngine in Main Window

First, we set up the data model and communication channel:

-   `model_` is assigned a new instance of `dataModel`, a custom class designed to manage the application's data. This class likely exposes data to both C++ and web ends via Qt's property system.

-   A `QWebChannel` object named `channel` is created. `QWebChannel` serves as a bridge for communication between C++ and JavaScript in the web view. The `dataModel` instance is registered with this channel using `registerObject`, making it accessible from the JavaScript side under the name `"dataModel"`.

Then, we configure the web view:

-   `webView_` is assigned a new instance of `QWebEngineView`, which will display web content within the application. The `webView_` is connected to the previously created `QWebChannel`.

-   The web view is set to load an HTML file (`chart.html`) from the application's resources using the `qrc:/` URL scheme, which accesses files embedded in the application's binary.

This setup creates a basic integrating web-based visualizations with C++ backend functionality in our Qt application.

```c++
// mainWindow.cpp

mainWindow::mainWindow(QWidget \*parent)
: QMainWindow(parent), webView*(nullptr), model*(nullptr) {

    model_ = new dataModel(this);

    auto channel = new QWebChannel(this);
    channel->registerObject(QStringLiteral("dataModel"), model_);

    webView_ = new QWebEngineView(this);
    webView_->page()->setWebChannel(channel);
    webView_->setUrl(QUrl("qrc:/chart.html"));

    auto randomButton = new QPushButton(this);
    randomButton->setText("Random");

    auto centralWidget = new QWidget(this);
    auto layout = new QVBoxLayout(centralWidget);
    layout->addWidget(webView_);
    layout->addWidget(randomButton);

    // ...
}
```

## Expose data and signal via dataModel

This section demonstrates how to create a data model class that exposes data to both C++ and JavaScript sides of the application using Qt's property system.

The essential setup for the `dataModel` class is defined as follows:

1. A `Q_PROPERTY` macro is used to expose the `dataSet_` member variable as a property named `dataSet`.

    - This property is of type `QJsonDocument`, allowing for flexible data structures.
    - The `MEMBER` keyword directly binds the property to the `dataSet_` member variable.
    - The `NOTIFY` keyword associates the property with the `dataSetChanged` signal.

2. A public `setData` method is provided to update the `dataSet_` and emit the `dataSetChanged` signal when data is changed on C++ side.

This setup allows for seamless data binding between C++ and JavaScript, with automatic notifications when the data changes.

```c++
// dataModel.hpp

class dataModel : public QObject {
    Q_OBJECT

    Q_PROPERTY(QJsonDocument dataSet MEMBER dataSet_ NOTIFY dataSetChanged);

public:
    explicit dataModel(QObject *parent = nullptr) : QObject(parent){};
    ~dataModel() override = default;

    void setData(const QJsonDocument &data) {
        dataSet_ = data;
        emit dataSetChanged();
    }

private:
    QJsonDocument dataSet_;

signals:
    void dataSetChanged();
};
```

## Integrating QWebChannel with Plotly

In our chart.html file, we have a simple HTML structure with a head and body. The head section loads two crucial scripts:

1. Plotly: A powerful library for creating interactive and visually appealing charts.
2. QWebChannel: A Qt-specific script that enables seamless communication between our C++ backend and JavaScript frontend.

We begin by establishing a connection to our dataModel object through QWebChannel. Once connected, we link the dataSetChanged signal from our dataModel to a function called onDataChanged. This setup ensures that whenever our data changes in C++, the onDataChanged function is automatically triggered.

The onDataChanged function is responsible for plotting the chart. It first clears any existing content in the plot area. Then, it retrieves the new data from our dataModel and structures it for use with Plotly. In this example, we're creating a 3D surface plot using x, y, and z data from our model.

To render the chart, we create a new div element, append it to our plot area, and use Plotly.newPlot to generate the 3D surface chart.

This implementation demonstrates a dynamic, data-driven 3D chart that updates automatically in response to changes in our C++ code. It showcases how Qt's QWebChannel can be leveraged to create responsive, interactive web content within Qt applications, bridging the gap between C++ backend logic and JavaScript frontend visualization.

```html
// chart.html

<head>
    <script src="qrc:/js/plotly"></script>
    <script src="qrc:/qtwebchannel/qwebchannel.js"></script>
</head>
<body>
    <div id="plot_area"></div>

    <script type="module">
        var dataModel;

        new QWebChannel(qt.webChannelTransport, function (channel) {
            dataModel = channel.objects.dataModel;
            dataModel.dataSetChanged.connect(onDataChanged);
        });

        var onDataChanged = function () {
            const plotArea = document.querySelector("#plot_area");

            while (plotArea.firstChild) {
                plotArea.removeChild(plotArea.firstChild);
            }

            var data = {
                x: dataModel.dataSet["x"],
                y: dataModel.dataSet["y"],
                z: dataModel.dataSet["z"],
                type: "surface",
            };

            const fig = document.createElement("div");
            plotArea.appendChild(fig);
            Plotly.newPlot(fig, [data]);
        };
    </script>
</body>
```

## Generate Data and Update Chart

Now that we have set up our web view and data model, let's bring everything together in our `mainWindow.cpp` file. We implement functionality to generate random data and ensure that initial data is created when the web view finishes loading.

The `randomData` function generates a mesh grid with x and y coordinates, along with random z values. This data is then set to the `dataModel` and triggers the `dataSetChanged` signal, which we discussed earlier. This mechanism allows for dynamic updates of the 3D surface plot in response to user actions or automatic triggers.

```c++
// mainWindow.cpp

mainWindow::mainWindow(QWidget *parent)
    : QMainWindow(parent), webView_(nullptr), model_(nullptr) {

    // ...

    auto randomButton = new QPushButton(this);
    randomButton->setText("Random");

    // ...

    connect(randomButton, &QPushButton::clicked, this, &mainWindow::randomData);

    connect(webView_, &QWebEngineView::loadFinished, this,
            &mainWindow::randomData);

}

void mainWindow::randomData() {
    // ...

    QJsonObject data;
    data["x"] = xArray;
    data["y"] = yArray;
    data["z"] = zArray;

    model_->setData(QJsonDocument{data});
}

```

## Conclusion

`QWebEngineView` is a powerful tool for embedding web content in your C++ applications. Whether you're building a simple browser, integrating web services, or creating hybrid applications, it offers a rich set of features to meet your needs. This blog has only scratched the surface, and there are many more capabilities and customization options available in `QWebEngineView`.

In future posts, we'll dive deeper into more advanced topics like customizing the rendering engine, handling web security, and optimizing performance. Stay tuned!

## Potential Pitfalls and Solutions

-   Deployment Issues: Ensure that QtWebEngineProcess.exe is present in the same directory as your application executable. This dependency is handled by the CMakeLists.txt configuration in this demonstration.

-   Building QWebEngine with VCPKG: When using VCPKG to build QWebEngine, certain MSVC components are required:

    -   Active Template Library (ATL)
    -   Microsoft Foundation Class (MFC)

    If these components are not installed. follow the steps:

    1. Open Visual Studio Installer
    2. Modify your Visual Studio installation
    3. Navigate to "Individual Components"
    4. Search for and select both ATL and MFC
    5. Install the selected components

## References

-   [Qt Documentation: QWebEngineView](https://doc.qt.io/qt-5/qwebengineview.html)
-   [Qt WebEngine Overview](https://doc.qt.io/qt-5/qtwebengine-index.html)
