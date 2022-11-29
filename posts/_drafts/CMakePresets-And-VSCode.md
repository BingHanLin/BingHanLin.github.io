---
title: Configure and build with CMake Presets in Visual Studio Code
tags:
  - Uncategorized
id: '2240'
---
# CMake presets
## Introduction
CMake presets are a collection of configuration, build and test options for a CMake project. These options are described in two JSON files named **CMakePreset.json** and **CMakeUserPresets.json** respectively. They both live in the project's root directory and have exactly the same schema. The difference between them is that the former is meant to specify **project-wide** build details, while the latter is meant for **developers own local build details**.

Therefore, the common options that shared with others are written in the **CMakePreset.json** and can be commited into version control. The specific options are defined by each developers in **CMakeUserPresets.json**, and for this reason, it’s important not to add **CMakeUserPresets.json** into version control.

This enables developers to share build knowledge both with others and with build instances such as continuous integration (CI).

## CMake Preset Sections
The CMake presets files are JSON documents with an object as the root and describe the following sections: 

* Configuration: The data that’s normally passed on the command line to the CMake executable. Examples of this include options, environment variables, toolchain information, and generator information (Visual Studio/Xcode projects).

* Build: A list of targets to build, along with other minor build options describing how to drive the compiler.

* Test: Instructions on how to execute CTest. Information such as which tests to run, how to output the results, and what to do when a failure occurs.

## CMake Presets Inheritance
A preset can inherit from another preset that is defined in the same file or in the files it **includes** with unlimited levels. The preset will inherit all of the fields from the inherits presets by default (except name description, and displayName), but can override them as desired.

If CMakePresets.json and CMakeUserPresets.json are both present in the same directory, CMakeUserPresets.json **implicitly includes** CMakePresets.json. Then presets in CMakePresets.json may be inherited by presets in CMakeUserPresets.json.

## Better Integration with IDEs
With CMake presets, all the dependencies and recipes are held in a parsable JSON format, meaning that tools can read them, too. Besides passing CMake presets to CMake CLI directly, many IDEs start to integrate CMake presets in their tools. Microsoft start CMake presets support in [Visual Studio 2019](https://learn.microsoft.com/en-us/cpp/build/cmake-presets-vs?view=msvc-170)  and [VS Code CMake plugin](https://github.com/microsoft/vscode-cmake-tools). JetBrains team also brings this feature to [CLion].(https://www.jetbrains.com/help/clion/cmake-presets.html).

Every developer can choose what text editors, IDEs, and tools they want to use to perform their job. That means we have many people working on/with different platforms, , etc.

All this means less setup for the developer, less chance of human error and making sure we’re all developing with reproducible results. The final directory structure will becomes:

```
----|
    |--

```


# Using CMake Presets in Visual Studio Code
In this secion, i will show you using Visual Studio Code and it extension to configurate and build a simple CMake project with CMake presets.

## Prerequisites
To complete the tutorial in the following section, install the following:
1. [Visual Studio Code](https://code.visualstudio.com/download).
2. [C++ extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools).
3. [CMake Tools extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools).
4. CMake 3.20 above.
5. Visual Studio build tool.


## Prepare CMake Porject

* Add a source code file: Create a new file and name the file **helloworld.cpp**.

  ``` cpp
  # helloworld.cpp

  #include <iostream>
  #include <vector>
  #include <string>

  using namespace std;

  int main()
  {
      vector<string> msg {"Hello", "C++", "World", "from", "VS Code", "and the C++ extension!"};

      for (const string& word : msg)
      {
          cout << word << " ";
      }
      cout << endl;
  }
  ```

* Add CMakeLists.txt: Create a CMakeLists.txt file in root directory with the following content.
  ``` cpp

  ```

Now, the directory structure looks like:
```
----|
    |--

```

## Enable CMake Preset option

First of all, you need to enablbe CMake preset option in CMake Tools settings section. Change the value to **always** to use CMake preset file explicitly.

| Setting | Description | Accepted values  |
|:--------:|:-------:|:------:|
| cmake.useCMakePresets    | Use CMakePresets.json to drive CMake configure, build, and test   | always, never, auto    |


## Configure CMake Project

# Reference
----------
https://github.com/microsoft/vscode-cmake-tools
https://code.visualstudio.com/docs/cpp/cmake-linux
https://www.nanoframework.net/build-updated-to-cmake-presets/
https://pspdfkit.com/blog/2021/cmake-presets-in-practice/
https://cmake.org/cmake/help/latest/manual/cmake-presets.7.html
