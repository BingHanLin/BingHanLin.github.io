---
title: 'OpenFOAM: Generate Mesh by SnappyHexMesh'
tags:
  - Uncategorized
id: '1695'
---

Introduction
------------

The **snappyHexMesh** tool built within **OpenFOAM** requires an existing geometry **base mesh** to work with. The base mesh usually comes from the blockMesh tool. The key steps involved when running snappyHexMesh are:

*   **Castellation:** The cells which are beyond a region set by a predefined point are deleted.
*   **Snapping:** Reconstructs the cells to move the edges from inside the region to the required boundary.
*   **Layering:** Creates additional layers in the boundary region.

* * *

Pre-processing
--------------

*   ### **Set-up of stl file  
    **
    
    Normally the .stl files are created using CAD software, such as CATIA and freeCAD. stl files contain information about the solid geometry. Create the **_triSurface_ folder** in the **_constant_** directory. It should contain a file with the geometry data to be meshed (stl, nas, obj). The file name is to be used as a reference pointer in later stages.
    
    _Note: The stl file should be in **ascii format**. All the stl files (different boundaries stl files) should form a **closed** geometry together._
    

*   ### **Set-up of Dict files  
    **
    
    The following files should be created in _**system directory**_ for using snappyHexMesh:
    
    1.  **blockMeshDict:  
        **A background mesh (base mesh) which surrounds the geometry surface (e.g. stl file) file is needed when using snappyHexMesh. Usually the background mesh is created by executing **blockMesh**. The background mesh will then be refined and removed based on the settings in the snappyHexMeshDict.
    2.  **snappyHexMeshDict:  
        **This file includes the settings of three steps (Castellation, Snapping, and Layering)  for running the snappyHexMesh.
    3.  **meshQualityDict:  
        **Includes parameters to be checked for mesh quality.
    4.  **decomposeParDict (optional):  
        **If the mesh is to be created in parallel mode using the decomposePar utility, this file defines the parameters for distributed processors.
    5.  **surfaceFeatureExtractDict (optional):  
        **Using surfaceFeatureExtract utility before meshing with snappyHexMesh helps to extract the sharp edges and have a better mesh with snappyHexMesh on these edges.

The following sections will focus on settings of three key steps in **snappyHexMeshDict**. And an example of using snappyHexMesh in a simulation is shown in the last section.

* * *

**snappyHexMeshDict**
---------------------

In the first section of this file you can set castellatedMesh, snap, addLayers to **true** or **false** depending on the stages required. The demonstration below only enables castellation stage to be executed.

castellatedMesh on;
snap            off;
addLayers       off;

Then all surfaces used by snappyHexMeshDict are listed in **geometry sub-dictionary** and each of them is named to be used as a reference in the later section.

geometry
{

  flange                  // name of surface
  {
    type triSurfaceMesh;  // type of surface
    file “flange.stl”;    // target stl file
  }

  refineHole              // name of surface
  {
    type searchableSphere;// type of surface (sphere)
    centre (0 0 -0.012);
    radius 0.003;
  }

};

Note: the basic user defined shapes are box, cylinder, sphere, plane and plate.

### Step1: **Castellation**

In the first step, the **castellatedMeshControls**, the initial mesh can be refined with levels. The level depends on the refinement set in the blockMesh, and the required refinement on the surfaces. Therefore, levels can be set in the sub-directories **features**, **refinementSurfaces** and **refinementRegions** in the **castellatedMeshControls**t.

castellatedMeshControls
{
    maxLocalCells 100000;
    maxGlobalCells 2000000;
    minRefinementCells 0;
    nCellsBetweenLevels 1;

    features
    (
        {
            file "flange.extendedFeatureEdgeMesh";
            level 0;
        }
    );

    refinementSurfaces
    {
        flange
        {
            level (2 2);
        }
    }
    
    resolveFeatureAngle 30;

    refinementRegions
    {
        refineHole
        {
            mode inside;
            levels ((1E15 3));
        }
        locationInMesh (-9.23149e-05 -0.0025 -0.0025);
        allowFreeStandingZoneFaces true;
    }
    
}

### Step2: **Snapping**

The second meshing stage is called “Snapping” where **patch faces are projected down onto the surface geometry**. Two important parameters are the number of mesh displacement iterations, **_nSolveIte_r** and the number of feature edge snapping iterations, **_nFeatureSnapIte_**r.

snapControls
{
   nSmoothPatch 3;
   tolerance 1.0;
   nSolveIter 300;
   nRelaxIter 5;
   nFeatureSnapIter 10;
   implicitFeatureSnap false;
   explicitFeatureSnap true;
   multiRegionFeatureSnap true;
}

### Step3: **Layering**

addLayersControls
{
    relativeSizes true;

    layers
    {
        "flange\_.\*"
        {
            nSurfaceLayers 3;
        }
    }

    expansionRatio 1.005;
    finalLayerThickness 0.3;
    minThickness 0.25;
    nGrow 0;
    featureAngle 30;
    nRelaxIter 5;
    nSmoothSurfaceNormals 1;
    nSmoothNormals 3;
    nSmoothThickness 10;
    maxFaceThicknessRatio 0.5;
    maxThicknessToMedialRatio 0.3;
    minMedianAxisAngle 90;
    nBufferCellsNoExtrude 0;
    nLayerIter 50;
    nRelaxedIter 20;
}

### Other settings:  
meshQualityControls, debugFlags, writeFlags

The mesh quality metrics used for the checks are set in the subdictionary **meshQualityControls**. During the process of snappyHexMesh, the mesh quality is constantly monitored. If a mesh motion or topology change causes a poor quality cell or face the motion or topology change is undone to revert the mesh back to a previously valid error free state.

At the end of the dictionary, you will find the sections: **debugFlags** and **writeFlags**. By default, they are commented. If you uncomment them, you will obtain the information that you can use to post process and troubleshoot the different steps of the meshing process.

* * *

Example
-------

* * *

https://openfoamwiki.net/images/f/f0/Final-AndrewJacksonSlidesOFW7.pdf

http://www.training.prace-ri.eu/uploads/tx\_pracetmo/snappyHexMesh.pdf

http://cfd.at/sites/default/files/tutorialsV4/12-ExampleTwelve.pdf

https://www.openfoam.com/documentation/user-guide/snappyHexMesh.php

https://www.cfd-online.com/Forums/openfoam-meshing/201972-snappyhexmesh-running-first-3-time-steps.html

http://www.wolfdynamics.com/wiki/meshing\_OF\_SHM.pdf

https://cfd.direct/openfoam/user-guide/v6-snappyhexmesh/