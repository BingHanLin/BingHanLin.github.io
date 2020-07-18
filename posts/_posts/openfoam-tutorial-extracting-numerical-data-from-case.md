---
title: 'OpenFOAM: Extracting Numerical Data From  Case'
tags:
  - My OpenFOAM Note
  - OpenFOAM
  - OpenFOAM
id: '1662'
date: 2019-04-23 11:24:09
---

Run-time data processing
------------------------

When we want to process data **during a simulation**, they need to configure the case accordingly. The two possible configuration processes are shown as follows, using an example of monitoring **flow rate** at an outlet patch named **outlet**.

### Method 1:

Firstly, we should include the flowRatePatch function in functions sub-dictionary in the case _controlDict_ file, using the _#includeFunc_ directive as follow.

functions 
{ 
    #includeFunc  flowRatePatch 
    //...  other function objects here ...//  
}

This configuration process will include the functionality in the flowRatePatch configuration file, located in the directory hierarchy beginning with $FOAM\_ETC/caseDicts/postProcessing.

The configuration of **flowRatePatch** requires the name of the patch to be supplied. To do this, we copy the **flowRatePatch file** into their case system directory. The _foamGet_ script can copy the file conveniently, e.g.

foamGet flowRatePatch

Now, we have a **flowRatePatch file** in the local case _system_ directory. The patch name can be edited in this **copied file** to be **outlet**. The solver will get an included function in the local case system directory, in precedence over the function in $FOAM\_ETC/caseDicts/postProcessing.

During the simulation, the flow rate through the patch **outlet** will be calculated and written out into a file within a directory named _postProcessing_ under the case directory.

### Method 2:

In this configuration process, we introduce another way to supply the name of the patch. Patch name can be easily specified by giving an **argument** to the **flowRatePatch** in the #includeFunc directive.

functions 
{ 
    #includeFunc  flowRatePatch(name=outlet) 
    //...  other function objects here ...//  
}

Some functions require the setting of many parameters, e.g. forces, forceCoeffs, surfaces, etc. For those functions, it is more reliable and convenient to copy and configure the function using method 1 rather than through arguments (method 2).

* * *

Post-processing of data
-----------------------

We can execute post-processing functions **after the simulation** is complete using the _postProcess_ utility. The same example of **flowRatePatch** function can be done by executing the following script in the terminal under the case directory.

postProcess -func "flowRatePatch(name=outlet)"

* * *

An example
----------

In the case of two-dimensional incompressible flow around an airfoil (see the airFoil2D case in tutorial directory ), we will record **residuals during the simulation** and obtain **force after the simulation**. The airfoil locates in the center of the rectangular domain with three inlet sides and one outlet side shown as follow.

![](https://bhlin.co.network/wp/wp-content/uploads/2019/03/5.png)

To obtain the residuals data, we need include the _residuals_ function in the _controlDict_ file.

functions 
{ 
    #includeFunc  residuals
    //...  other function objects here ...//  
}

The default fields that residuals function captures are _p_ and _U_. If we wish to get other fields, we should either make copy the _residuals_ file in their _system_ and edit the fields entry (method 1) or define the **arguments** to the residuals function in the _controlDict_ file (method 2).

When the function is executed **during a simulation**, we may wish to monitor the data **live on screen**. To do this, we need to run the _foamMonitor_ script (i will explain it in next note) in the terminal as follow.

 foamMonitor -l postProcessing/residuals/0/residuals.dat

If the command is executed before the simulation is complete, then we can see the graph being updated live.

![](https://bhlin.co.network/wp/wp-content/uploads/2019/04/螢幕快照-2019-04-04-095045.png)

![](https://bhlin.co.network/wp/wp-content/uploads/2019/04/螢幕快照-2019-04-04-095054.png)

Note: The simpleFoam is the steady state solver. The axis "Time" here means the number of the iteration.

After the simulation, we want to extract the **force** act on the airfoil. The _forcesIncompressible_ function can help us get the force data from the case. Let's type the command below in the terminal.

simpleFoam -postProcess -func "forcesIncompressible(patches=(foilwalls))"

This command is slightly different with the one we mention [above](#postprocessing). To who interest in the detail of the command in this form can refer to the [CFD Direct](https://cfd.direct/openfoam/user-guide/v6-post-processing-cli/#x31-2500006.2.4).

The force data then can be found in the forces.dat in postProcessing directory. In the _forces.dat_ we have tuple which holds the pressure, viscous and porous forces/moments act on the airfoil with 3 dimensions.

![](https://bhlin.co.network/wp/wp-content/uploads/2019/04/螢幕快照-2019-04-04-104422-1-1024x283.png)

* * *

*   Reference:

1.  [Post-Processing CLI](https://cfd.direct/openfoam/user-guide/v6-post-processing-cli/)
2.  [Tutorial of how to plot residuals !](https://www.cfd-online.com/Forums/openfoam-community-contributions/64146-tutorial-how-plot-residuals.html)
3.  [Lift and Drag Study of an Airfoil](https://n.ethz.ch/~aluecker/toolscourse/html-chunk/sect1_lift_drag_study.html)
4.  [OpenFOAM : Run-time post-processing](http://hmf.enseeiht.fr/travaux/projnum/book/export/html/901)