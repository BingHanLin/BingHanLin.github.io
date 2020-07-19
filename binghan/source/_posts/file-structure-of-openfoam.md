---
title: File Structure of OpenFOAM
tags:
    - OpenFOAM
categories: 
    - OpenFOAM Note
id: '892'
date: 2018-06-11 19:15:22

---

Installation directory
----------------------

Let's start from the installation dirctory, you can use the Linux command **"tree"** to examine the source code directory organization.
<!-- more -->
    tree -d -L 1 $WM_PROJECT_DIR
    

This show you the folders in the `$WM_PROJECT_DIR`(installation dirctory). You can also find other files in this directory, but most importantly one is **Allwmake** which compiles all of OpenFOAM by calling other Allwmake scripts. All the directories are introduced as follow: 

![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/openfoam-structure.jpg)

1.  **applications:** The directory contains the source files of all the executables which is created using the **C++** libraries. Here is a short description of the directories under applications .
    *   **solvers** Contains source code for the distributed solvers.
    *   **tests** Contains source code that test and show example of the usage of some OpenFOAM libraries.
    *   **Utilities** Contains source code to perform pre- and post-processing tasks involving data manipulations and algebraic manipulations.

> note: there is also an **Allwmake** script, which will compile all the contents of **solvers** and **utilities**.

2.  **tutorials:** Contains tutorials that demonstrate thr usage of all solvers and most of the utilities.
    
3.  **src:** The src directory contains several subdirectories which include the the source code for all the libraries. The important folders are:
    
    *   **finiteVolume** This library provides all the classes needed for the finiteVolume discretization, such as the fvMesh class, finiteVolume discretization operators (divergence, laplacian, gradient, and fvc/fvm), and boundary conditions (`fields/fvPatchFields`). In `cfdTools/general/include/` you also find the very important file fvCFD.H, which is included in most applications.
    *   **OpenFOAM** This core library includes the definitions of the containers used for the operations, the field definitions, the declaration of the mesh and of all the mesh features such as zones and sets.
    *   **turbulenceModels** Contains many libraries for turbulence models.
4.  **bin:** The bin directory contains shell scripts, such as paraFoam,foamNew, foamLog...
    
5.  **doc:** The doc directory contains the documentation of OpenFOAM, such as Programmers Guide, User Guide, and Doxygen generated documentation in html format etc.
    
6.  **doc:** The doc directory contains the documentation of OpenFOAM, such as Programmers Guide, User Guide, and Doxygen generated documentation in html format etc.
    
7.  **etc:** Theetcdirectory contains environment set-up files, global **_controlDict_**, and default **_thermoData_**.
    
8.  **platforms:** Contains the binaries of the applications (bin) and dynamic libraries.
    
9.  **wmake:** **Compiler settings** are included in this directory incluiding optimisation flags. It also contains **_wmake_**, a special make command which understand the OpenFOAM file structure.
    

* * *

Case directory (Working diretory)
---------------------------------

The basic directory structure for a OpenFOAM case, that contains the minimum set of files required to run an application, is shown in following figure and described as follows:

![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/user281x.png) Source : https://cfd.direct/openfoam/user-guide/case-file-structure

*   **constant** Contains a full description of the case **mesh** in a subdirectory polyMesh and files specifying physical properties for the application concerned, e.g. transportProperties.
*   **system** For setting parameters associated with the solution procedure itself. It contains at least the following 3 files: **_controlDict_** where run control parameters are set including start/end time, time step and parameters for data output; **_fvSchemes_** where discretisation schemes used in the solution may be selected at run-time; and, **_fvSolution_** where the equation solvers, tolerances and other algorithm controls are set for the run.
*   **time (or 0)** Containing individual files of data for particular fields, e.g. velocity and pressure. The data can be: either, initial values and boundary conditions that the user must specify to define the problem; or, results written to file by OpenFOAM. The name of each time directory is based on the simulated time at which the data is written. It is sufficient to say now that since we usually start our simulations at time t = 0, the initial conditions are usually stored in a directory named 0 or 0.000000e+00, depending on the name format specified. For example, in the cavity tutorial, the velocity field U and pressure field p are initialised from files 0/U and 0/p respectively.

* * *

Run tutorials in OpenFOAM
-------------------------

For OpenFOAM users, tutorials are essential because in most cases you will start your own project by:

*   Selecting a solver which implements all necessary physics
*   Checking the tutorials available for the solver
*   Copying, renaming and modifying the most similar tutorial
*   Testing and running your own simulation

However, the tutorial collection contains a variety of different case setups. In the following, three different ways to run these tutorials are introduced.

*   **Simple blockMesh/mySolverFoam tutorials**
*   **Tutorials with Allrun/Allclean scripts**
*   **Tutorials which require system operations**

Thses 3 ways are briefly descrided as follow, see this [article](http://myheutagogy.com/2016/03/17/of_tutorials/) for further detail.

1.  **Simple blockMesh/mySolverFoam tutorials** For a common case such as lid-driven cavity flow (you can find it in `$FOAM_RUN/tutorials/incompressible/icoFoam/cavity/`), the directory contains **system**, **constant**, and **0**. If no further execution scripts are provided, you will always have to run `blockMesh`, for the mesh creation, and afterwards your solver of choice, `icoFoam` in our case . A possible scenario is an additional **setFieldsDict** to set initial field values. The corresponding utility to run after `blockMesh` would be `setFields`.
    
    `blockMesh = >> setFields (if need)= >> icoFoam(choose your solver)`
    
2.  **Tutorials with Allrun/Allclean scripts** For some complicated cases, automating processes comes naturally within a Linux environment via Shell scripts. Basically, all necessary commands are written into a file which is then executed. In the tutorial collection these scripts are usually called **_Allrun_**.
    
3.  **Tutorials which require system operations** “System operations” basically means that an application (e.g. a solver) compiles and (hopefully) runs user-supplied C++ source code at runtime. Examples are the [#codeStream](https://openfoam.org/release/2-0-0/run-time-control-code-compilation/) directive or the codedFixedValue boundary condition.
    

* * *

*   Reference:

1.  [OpenFOAM基础培训-目录结构](https://wenku.baidu.com/view/efbee181fe4733687f21aa6a.html)
2.  [Introduction to OpenFOAM](http://www.hpc.lsu.edu/training/weekly-materials/2016-Spring/intro_of_20160224.pdf)
3.  [OpenFOAM directory organization](http://www.tfd.chalmers.se/~hani/kurser/OS_CFD_2015/directoryOrganization.pdf)
4.  [OpenFOAM for beginners: Hands-on training](https://www.slideshare.net/JibranHaider/openfoam-for-beginners?)
5.  [CFD Direct](https://cfd.direct/openfoam/user-guide/case-file-structure/)
6.  [aleigus的博客-Openfoam学习记录](https://blog.csdn.net/aleigus/article/details/72917112)
7.  [3 ways to run tutorials in OpenFOAM](http://myheutagogy.com/2016/03/17/of_tutorials/)