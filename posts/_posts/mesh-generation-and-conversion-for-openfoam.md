---
title: Mesh Generation and Conversion for OpenFOAM
tags:
  - My OpenFOAM Note
  - OpenFOAM
  - OpenFOAM
id: '1126'
date: 2018-06-15 17:06:22
---

Mesh description
----------------

### Mesh Specification and Validity Constraints

The conditions that a mesh must satisfy are:

1.  **Points:** A point is a location in **3-D space**, defined by a vector in units of metres (m). The points are compiled into a list and each point is referred to by a label, which represents its position in the list, **starting from zero**.
    
2.  **Faces:** Faces are compiled into a list and each face is referred to by its label, representing its position in the list. The direction of the face normal vector is defined by the **right-hand rule** as shown in Figure below. The ordering of point labels in a face is such that each two neighbouring points are connected by an edge.
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/user350x.png)  Face area vector from point numbering on the face (Source : https://cfd.direct/openfoam/user-guide/mesh/)
    
    There are two types of face:
    *   **Internal faces** Those faces that connect two cells (and it can never be more than two). The face normal points **into the cell with the larger label**.
    *   **Boundary faces** Those belonging to one cell since they coincide with the boundary of the domain. A boundary face is therefore addressed by one cell(only) and a boundary patch. The face normal points **outside of the computational domain**.
3.  **Cells:** A cell is a list of faces in arbitrary order. Cells must have the properties of **Contiguous**, **Convex**, and **Closed**.
    
4.  **Boundary** A boundary is a list of patches, each of which is **associated with a boundary condition**. A patch is a list of face labels which clearly must contain **only boundary faces** and no internal faces.
    

### The polyMesh description

![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/user281x.png) Source : https://cfd.direct/openfoam/user-guide/case-file-structure

As we mentioned in [previous article](https://bhlin.co.network/wp/2018/06/11/file-structure-of-openfoam/#Case_directory_Working_diretory), the **_constant_** directory contains a full description of the case mesh in a subdirectory **_polyMesh_**. The **_polyMesh_** description is based around faces. Each face (internal) is therefore assigned an ‘owner’ cell and ‘neighbour’ cell so that the connectivity across a given face can simply be described by the owner and neighbour cell labels. In the case of boundaries, the connected cell is the owner and the neighbour is assigned the label ‘-1’. The files in directory **_polyMesh_** are discussed below:

*   **points** A list of vectors describing the cell vertices (index: 0, 1, 2,...).
*   **faces** A list of faces, each face being a list of indices to vertices in the points list (index: 0, 1, 2,...).
*   **owner** A list of **owner cell labels**, the index of entry relating directly to the index of the face, so that the first entry in the list is the owner label for face 0, the second entry is the owner label for face 1, etc;
*   **neighbour** A list of neighbour cell labels.
*   **boundary** A list of patches, containing a dictionary entry for each patch, declared using the **patch name**, e.g.

    movingWall 
    { 
        type patch; 
        nFaces 20; 
        startFace 760; 
    }
    

> 　Read more: [Cell shapes, 1-Ｄ 2-Ｄ and axi-symmetric problems](https://bhlin.co.network/wp/?p=1126&preview=true)

* * *

Boundaries
----------

A boundary is generally broken up into a set of **patches**. One patch may include one or more enclosed areas of the boundary surface which do **not necessarily need to be physically connected**. A **type** is assigned to every patch as part of the mesh description.

### Geometric (constraint) patch 'types'

Only some types in OpenFOAM are summarised below. This is not a complete list; for all types see `$FOAM_SRC/finiteVolume/fields/fvPatchFields/constraint`.

*   **patch:** generic type containing no geometric or topological information about the mesh, e.g. used for an inlet or an outlet.
*   **wall:** for patch that coincides with a solid wall, required for some physical modelling, e.g. wall functions in turbulence modelling.
*   **symmetryPlane:** for a planar patch which is a symmetry plane.
*   **symmetry:** for any (non-planar) patch which uses the symmetry plane (slip) condition.
*   **empty:** for solutions in in 2 (or 1) dimensions (2D/1D), the type used on each patch whose plane is normal to the 3rd (and 2nd) dimension for which no solution is required.
*   **wedge:** for 2 dimensional axi-symmetric cases.

### Boundary conditions

Boundary conditions are specified in field files, e.g. **_p_**, **_U_**. Every patch includes a type entry that specifies the type of boundary condition. Only some boundary condition types available in OpenFOAM are listed below using a patch field named \[latex\]Q\[/latex\]. For all types see `$FOAM_SRC/finiteVolume/fields/fvPatchFields/basic`.

*   **fixedValue:** value of \[latex\]Q\[/latex\] is specified by value.
*   **fixedGradient:** normal gradient of \[latex\]Q\[/latex\] (\[latex\]\\frac{Q}{n}\[/latex\]) is specified by gradient.
*   **zeroGradient:** normal gradient of \[latex\]Q\[/latex\] is zero.
*   **calculated:** patch field \[latex\]Q\[/latex\] calculated from other patch fields.
*   **mixed:** mixed fixedValue/ fixedGradient condition depending on valueFraction (0 ≤ valueFraction ≤ 1).
*   **directionMixed:** mixed condition with tensorial valueFraction, to allow different conditions in normal and tangential directions of a vector patch field, e.g. fixedValue in the tangential direction, zeroGradient in the normal direction.

> 　Read more: [more complex boundary conditions](https://cfd.direct/openfoam/user-guide/boundaries/#x24-1710005.2)

* * *

Mesh generation with the **_blockMesh_** utility
------------------------------------------------

The mesh is generated from a dictionary file named **_blockMeshDict_** located in the \*\*system\*\*\* (or \*\*\*constant/polyMesh\*\*\*) directory of a case. \*\*\*BlockMesh\*\*\* reads this dictionary, generates the mesh and writes out the mesh data to points and faces, cells and boundary files in the same directory. **_BlockMesh_** will decompose the domain geometry into a set of one or more 3-D, hexahedral blocks. Each block of the geometry is defined by **8 vertices**, one at each corner of a hexahedron. Edges of the blocks can be **straight lines, arcs or splines**. Each block has a local coordinate system \[latex\](x\_1,x\_2,x\_3)\[/latex\] that must be right-handed. The local coordinate system is defined by the order in which the vertices are presented in the block definition according to:

*   the axis origin is the first entry in the block definition, vertex 0 in our example;
*   the x1 direction is described by moving from vertex 0 to vertex 1;
*   the x2 direction is described by moving from vertex 1 to vertex 2;
*   vertices 0, 1, 2, 3 define the plane \[latex\]x\_3\[/latex\] = 0;
*   vertex 4 is found by moving from vertex 0 in the \[latex\]x\_3\[/latex\] direction;
*   vertices 5,6 and 7 are similarly found by moving in the \[latex\]x\_3\[/latex\] direction from vertices 1,2 and 3 respectively.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/user379x.png) A single block (Source : https://cfd.direct/openfoam/user-guide/blockmesh/).

### Writing a blockMeshDict file

The **_blockMeshDict_** file is a dictionary using keywords described below.

*   **convertToMeters:** scaling factor for the vertex coordinates, e.g. 0.001 scales to mm.
*   **vertices:** list of vertex coordinates.
*   **edges:** used to describe curved geometry.
*   **block:** ordered list of vertex labels and mesh size.
*   **boundary:** subdictionary of boundary patches.
*   **mergePatchPairs:** list of patches to be merged.

A breifly introduction for every keywords are described below, see [here](https://cfd.direct/openfoam/user-guide/blockMesh/#x25-1800005.3.1) for further detail configurations of each keywords.

1.  The **convertToMeters**: Keyword specifies a scaling factor by which all vertex coordinates in the mesh description are multiplied. For example,

    convertToMeters    0.001;
    

2.  The **vertices**: The vertices of the blocks of the mesh are given next as a standard list named **_vertices_**. For example,

    vertices 
        ( 
            ( 0    0    0  )    // vertex number 0 
            ( 1    0    0.1)    // vertex number 1 
            ( 1.1  1    0.1)    // vertex number 2 
            ( 0    1    0.1)    // vertex number 3 
            (-0.1 -0.1  1  )    // vertex number 4 
            ( 1.3  0    1.2)    // vertex number 5 
            ( 1.4  1.1  1.3)    // vertex number 6 
            ( 0    1    1.1)    // vertex number 7 
        );
    

3.  The **edges**: Each edge joining 2 vertex points is assumed to be **straight by default**. However it could be **curved** by entries in a list named edges (arc, spline, etc.). The list is optional; if the geometry contains no curved edges, it may be omitted.
    
4.  The **blocks**: The block definitions are contained in a list named **_blocks_**. Each block definition is a compound entry consisting of **(1)**　a list of vertex labels, **(2)** a vector giving the number of cells required in each direction, **(3)** the type and list of cell expansion ratio in each direction. For example,
    

        blocks 
        ( 
            hex (0 1 2 3 4 5 6 7)    // vertex numbers 
            (10 10 10)               // numbers of cells in each direction (x1, x2, x3)
            simpleGrading (1 2 3)    // cell expansion ratios (simpleGrading or edgeGrading)
        );
    

**Multi-grading of a block** is avaiable in OpenFOAM v2.4+. It can divide a block in an given direction and apply different grading within each division. A example is shown below:

    blocks 
    ( 
        hex (0 1 2 3 4 5 6 7) (100 300 100) 
        simpleGrading (1 2 3); 
    );
    

See [here](https://cfd.direct/openfoam/user-guide/blockMesh/#x25-1800005.3.1) for further detail.

5.  The **boundary**: The boundary of the mesh is given in a list named **_boundary_**. The boundary is broken into patches (regions), where each patch in the list has its name as the keyword, which is the choice of the user. The patch information is then contained in sub-dictionary with:

*   **type**: the patch type, either a generic **_patch_** on which some boundary conditions are applied or a particular geometric condition.
*   **faces**: a list of block faces that make up the patch.

### Running blockMesh

As described before, the following can be executed at the command line to run blockMesh for a case in the directory:

    blockMesh -case <case>
    

> Read more: [(1) Multiple blocks, (2) Naming vertices, edges, faces and blocks, etc.](https://cfd.direct/openfoam/user-guide/boundaries/#x24-1710005.2)

* * *

Mesh generation with the snappyHexMesh utility
----------------------------------------------

The **_snappyHexMesh_** utility generates 3-dimensional meshes containing hexahedra (hex) and split-hexahedra (split-hex) automatically. The mesh approximately conforms to the surface by iteratively refining a starting mesh and morphing the resulting split-hex mesh to the surface.

### Mesh generation process of **_snappyHexMesh_**

In order to run **_snappyHexMesh_**, the user requires the following:

*   One or more tri-surface files located in a constant/triSurface sub-directory of the case directory.
*   A background hex mesh which defines the extent of the computational domain and a base level mesh density; typically generated using **_blockMesh_**.
*   A snappyHexMeshDict dictionary, with appropriate entries, located in the system sub-directory of the case.

The mesh generation process of **snappyHexMesh** usually includes the following steps:

1.  **Creating the background hex mesh:** Before **_snappyHexMesh_** is executed the user must create a background mesh of hexahedral cells that fills the entire region within by the external boundary.
2.  **Cell splitting at feature edges and surfaces:** The splitting process begins with cells being selected according to specified edge features first within the domain. Following feature refinement, cells are selected for splitting in the locality of specified surfaces.
3.  **Cell removal:** Once the feature and surface splitting is complete a process of cell removal begins. Cell removal requires one or more regions enclosed entirely by a bounding surface within the domain. Cells are retained if, approximately speaking, 50% or more of their volume lies within the region.
4.  **Cell splitting in specified regions:**  
    Cells that lie within one or more specified volume regions can be further split.
5.  **Snapping to surfaces:** Moving cell vertex points onto surface geometry to remove the jagged castellated surface from the mesh.
6.  **Mesh layers:** An optional stage of the meshing process which introduces additional layers of hexahedral cells aligned to the boundary surface.
7.  **Mesh quality controls:** Mesh quality is controlled by the entries in the **_meshQualityControls_** sub-dictionary in **_snappyHexMeshDict_**.
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/圖片1-2.png) Source : https://cfd.direct/openfoam/user-guide/snappyHexMesh/
    

* * *

Conversion mesh generated by a third-party software
---------------------------------------------------

The user can generate meshes using other packages and convert them into the format that OpenFOAM uses. Some of the more popular mesh converters are listed below.

*   **fluentMeshToFoam:** reads a Fluent.msh mesh file, working for both 2-D and 3-D cases;
*   **starToFoam** reads STAR-CD/PROSTAR mesh files.
*   **gambitToFoam:** reads a GAMBIT.neu neutral file;
*   **ideasToFoam:** reads an I-DEAS mesh written in ANSYS.ans format;
*   **cfx4ToFoam:** reads a CFX mesh written in .geo format;

I only presented the guides of packages that i have used in this section. See [here](https://cfd.direct/openfoam/user-guide/mesh-conversion/) for further detail.

### fluentMeshToFoam

**_Fluent_** writes mesh data to a single file with a .msh extension. The file must be written in ASCII format, which is not the default option in **_Fluent_**. It is possible to convert single-stream **_Fluent_** meshes. When reading a 2 dimensional **_Fluent_** mesh, the converter automatically extrudes the mesh in the third direction and adds the empty patch, naming it **_frontAndBackPlanes_**. **Note the following features!**

*   The OpenFOAM converter will attempt to capture the **_Fluent_** boundary condition definition as much as possible; however, since there is no clear, direct correspondence between the OpenFOAM and **_Fluent_** boundary conditions, the user should **check the boundary conditions before running a case**.
*   Creation of axi-symmetric meshes from a 2 dimensional mesh is currently not supported but can be implemented on request.
*   **Multiple material meshes are not permitted**. If multiple fluid materials exist, they will be converted into a single OpenFOAM mesh; if a solid region is detected, the converter will attempt to filter it out.
*   Fluent allows the user to define a patch which is internal to the mesh, i.e. consists of the faces with cells on both sides. Such patches are not allowed in OpenFOAM and the converter will attempt to filter them out.
*   There is currently no support for embedded interfaces and refinement trees.

The procedure of converting a **_Fluent.msh_** file is first to create a new OpenFOAM case by creating the necessary directories/files: the case directory containing a **_controlDict_** file in a **_system_** subdirectory. Then at a command prompt the user should execute:

    fluentMeshToFoam <meshFile>
    

where is the name of the **_.msh_** file, including the full or relative path.

### gambitToFoam

**_GAMBIT_** writes mesh data to a single file with a **_.neu_** extension. The procedure of converting a **_GAMBIT.neu_** file is first to create a new OpenFOAM case, then at a command prompt, the user should execute:

     gambitToFoam <meshFile>
    

where is the name of the **_.neu_** file, including the full or relative path. The **_GAMBIT_** file format does not provide information about type of the boundary patch, e.g. wall, symmetry plane, cyclic. Therefore **all the patches have been created as type patch**. Please reset after mesh conversion as necessary.

* * *

*   Reference:

1.  [CFD Direct](https://cfd.direct/openfoam/user-guide/mesh/)
2.  [Mesh generation with the blockMesh utility](https://www.openfoam.com/documentation/user-guide/blockMesh.php)
3.  [Mesh generation with the snappyHexMesh utility](https://www.openfoam.com/documentation/user-guide/snappyHexMesh.php)
4.  [Generating Mesh using snappyHexMesh](http://spoken-tutorial.org/watch/OpenFOAM/Generating+Mesh+using+snappyHexMesh/English/)
5.  [snappyHexMesh Tutorial](https://www.youtube.com/watch?v=cJuRoTd2psA)
6.  [A tool for pre-processing: snappyHexMesh](http://www.training.prace-ri.eu/uploads/tx_pracetmo/snappyHexMesh.pdf)