---
title: 'OpenFOAM: Sampling and Monitoring Data'
tags:
    - OpenFOAM
categories: 
    - OpenFOAM Note
id: '1672'
date: 2019-04-04 08:32:02
---

There are a set of general post-processing functions for sampling data across the domain for graphs and visualization. In this article, we use the *lid-driven cavity* case set up in the tutorial to demonstrate these post-processing functions.

<!-- more -->

* * *

Probing data
------------

When we want to get the time series data of the fields on certain point locations, the functions **boundaryCloud**, **internalCloud,** and **probes** can help us. All functions work on the basis that the user provides some point locations and a list of fields, and the function writes out values of the fields on those locations in each time interval.

We use the [method](https://bhlin.co.network/wp/2019/04/04/openfoam-tutorial-extracting-numerical-data-from-case/#method1) mention in the previous post to include the functions. The configuration is started by adding the #includeFunc directive to functions in the _controlDict_ file.

    functions 
    { 
        #includeFunc  probes 
        ...  other function objects here ...  
    }

The **probes** function is configured by copying the file to the local system directory using **foamGet**.

    foamGet probes

Let's say we want to obtain the pressure and velocity value on certain locations, then specify the locations we need in probeLocations in the **probes** file as follows.

    #includeEtc "caseDicts/postProcessing/probes/probes.cfg"
    
    fields (p U);
    probeLocations
    (
        (0 0 0) // point 1
        (0 0.5 0) // point 2 ...
    );

When the simulation is running, time-value data is written into _p_ and _U_ files in _postProcessing/probes/0_.

![](https://bhlin.co.network/wp/wp-content/uploads/2019/04/螢幕快照-2019-04-15-160315.png)

The pressure data record by **probes** function.

* * *

Sampling line data
------------------

The _singleGraph_ function samples data from a line defined by the user. Again, we add the #includeFunc directive to functions in the _controlDict_ file.

    functions 
    { 
        #includeFunc  singleGraph 
        ...  other function objects here ...  
    }

Copy the configuration file of the _singleGraph_ function using **foamGet**.  

    foamGet singleGraph

In the configuration file we can specify:

*   The start and end points of the line where data is sampled.
*   The fields need to be sampled.
*   The type of sampling.

In the configuration below, the _singleGraph_ function will extract velocity and pressure data from the 100 uniform distributed data points on the line. During the simulation, distance-value data is written into files in time directories within _postProcessing/singleGraph_.

    start   (0.05 0 0);
    end     (0.05 0.1 0);
    fields  (U p);

    // Sampling and I/O settings
    #includeEtc "caseDicts/postProcessing/graphs/sampleDict.cfg"

    // Override settings here, e.g.
    setConfig
    {
        type    lineUniform; // lineCell, lineCellFace
        axis    distance;    // x, y, z, xyz
        nPoints 100;
    }

    // Must be last entry
    #includeEtc "caseDicts/postProcessing/graphs/graph.cfg"

We can quickly display the data for x-component of velocity, last time (0.5 in my case), by running gnuplot with the following commands.

    gnuplot 
    gnuplot> set style data linespoints 
    gnuplot> plot "postProcessing/singleGraph/0.5/line_U.xy" u 2:1

![](https://bhlin.co.network/wp/wp-content/uploads/2019/04/DD.png)

The x-component of velocity along the line.

* * *

Sampling surface data
---------------------

The _surfaces_ functions can be used to generate files for visualization. First, add the #includeFunc directive to functions in the _controlDict_ file.

    functions 
    { 
        #includeFunc  surfaces 
        ...  other function objects here ...  
    }

The target surface can be specified by **cutting plane**, **isosurface**, **patch surface**. The _surfaces_ function is configured by copying the _surfaces_ file to the _system_ directory using _foamGet_.

    foamGet surfaces

In this demonstration, we specify the target surface by **cutting plane** which the base point and normal vector should be edited.

    #includeEtc "caseDicts/postProcessing/visualization/surfaces.cfg"
    
    fields       (p U);
    
    surfaces
    (
        zNormal
        {
            $cuttingPlane;
            pointAndNormalDict
            {
                basePoint    (0.05 0.05 0); // Overrides default basePoint (0 0 0)
                normalVector $z;      // $z: macro for (0 0 1)
            }
        }
    
    
    );

Then surfaces function produces VTK format files of the cutting plane with pressure and velocity data in time directories in the the _postProcessing/surfaces_ directory. The user can display the cutting plane by opening these VTK files in _ParaView_ (type paraview).

![](https://bhlin.co.network/wp/wp-content/uploads/2019/04/DD-1.png)

Visualization of velocity data from VTK file.

* * *

Live monitoring of data
-----------------------

To monitor the data during the simulation, the user should then run _foamMonitor_ the terminal. If the command is executed before the simulation is complete, then we can see the graph being updated live.

Firstly, include the _residuals_ function in the _controlDict_ file.  

        functions 
        { 
            #includeFunc  residuals 
            ...  other function objects here ...  
        }

The default fields whose residuals are captured are _p_ and _U_. If we wish to get other fields, we should either make copy the _residuals_ file in their _system_ and edit the fields entry (method 1) or define the **arguments** to the residuals function in the _controlDict_ file (method 2). Here, we use the method 1. The _residuals_ file can then be copied into the _system_ directory conveniently using _foamGet_:

    foamGet residuals

It is advisable to delete the _postProcessing_ directory to avoid duplicate files for each function. The user can delete the directory, then run simulation **in the background**.

    rm -rf postProcessing
    icoFoam > log &

Then run _foamMonitor_ before the simulation is complete.

    foamMonitor -l postProcessing/residuals/0/residuals.dat

![](https://bhlin.co.network/wp/wp-content/uploads/2019/04/Webp.net-gifmaker.gif)

The graph being updated live.

* * *

*   Reference:

1.  [Examples of how to use some utilities and functionObjects](https://pingpong.chalmers.se/public/pp/public_courses/course07056/published/1497955220499/resourceId/3711490/content/UploadedResources/someUtilitiesAndFunctionObjects.pdf)
2.  [Tutorial of how to plot residuals !](https://www.cfd-online.com/Forums/openfoam-community-contributions/64146-tutorial-how-plot-residuals.html)
3.  [OpenFOAM :](http://hmf.enseeiht.fr/travaux/projnum/book/export/html/901) [Graphs and Monitoring](https://cfd.direct/openfoam/user-guide/v6-graphs-monitoring/)