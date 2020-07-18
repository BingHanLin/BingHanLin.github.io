---
title: '[Lecture Notes] Advanced Computation Methods for Fluid Flow – 05'
tags:
  - Advanced Computation Methods for Fluid Flow - 2018
  - computational fluid dynamics
  - numerical method
id: '489'
date: 2018-04-03 23:44:04
---

> _28/03/2018, Chapter2 - General Curvilinear Coordinates_

* * *

General Curilinear Coordinates
------------------------------

Consider a position vector \[latex\]\\vec{r}=\\vec{r}(\\xi^1,\\xi^2,\\xi^3)\[/latex\] in curvilinear coordinates.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名.png)

*   **Covariant base vectors** Use chain rules of differentiation:
    
    \[latex\]\\eqalign{ d\\vec{r}=\\frac{\\partial\\vec{r}}{\\partial \\xi^1}d\\xi^1+\\frac{\\partial\\vec{r}}{\\partial \\xi^2}d\\xi^2+\\frac{\\partial\\vec{r}}{\\partial \\xi^3}d\\xi^3 \\\\=d\\xi^1\\vec{a}\_1+d\\xi^2\\vec{a}\_2+d\\xi^3\\vec{a}\_3=d\\xi^i\\vec{a}\_i }\[/latex\]
    
    where \[latex\]\\frac{\\partial \\vec{r}}{\\partial \\xi^i}\[/latex\] is the change of \[latex\]\\vec{r}\[/latex\] in \[latex\]\\xi^i\[/latex\] direction. Therefore, \[latex\]\\vec{a}\_i\[/latex\] are covariant base vectors.
    
*   **Contravariant velocities** Velocity vectors is defined by
    
    \[latex\]\\eqalign{ \\vec{v}=\\frac{d\\vec{r}}{dt}= \\frac{\\partial\\vec{r}}{\\partial \\xi^1}\\frac{d\\xi^1}{dt} +\\frac{\\partial\\vec{r}}{\\partial \\xi^2}\\frac{d\\xi^2}{dt} +\\frac{\\partial\\vec{r}}{\\partial \\xi^3}\\frac{d\\xi^3}{dt} \\\\=\\frac{\\partial\\vec{r}}{\\partial \\xi^i}\\frac{d\\xi^i}{dt}=v^i\\vec{a}\_i }\[/latex\]
    
    where \[latex\]v^i\[/latex\] is the contravariant velocity component along \[latex\]\\xi^i\[/latex\] - direction. (parallel to \[latex\]\\vec{r}\[/latex\])
    
*   **Differential volume** Differential volume:
    
    \[latex\]\\eqalign{ d\\Omega=(d\\xi^1\\vec{a}\_1)\\cdot(d\\xi^2\\vec{a}\_2 \\times d\\xi^3\\vec{a}\_3)=\\\\(d\\xi^1d\\xi^2d\\xi^3)\\ \\vec{a}\_1\\cdot(\\vec{a}\_2 \\times \\vec{a}\_3) =Jd\\xi^1d\\xi^2d\\xi^3 }\[/latex\]
    
    Length of a differential element is defined by:
    
    \[latex\]\\eqalign{ \[(d\\xi^i\\vec{a}\_i)\\cdot(d\\xi^i\\vec{a}\_i)\]=d\\xi^i(\\vec{a}\_i\\cdot\\vec{a}\_i)^\\frac{1}{2} \\quad (\\textrm{no sum on i}) }\[/latex\]
    
    **For general curvilinear coordinate: \[latex\]\\sqrt{g\_{ii}}d\\xi^i\[/latex\]** **For orthogonal coordinate: \[latex\]h\_id\\xi^i\[/latex\]**
    

* * *

Tensors in General Curilinear Coordinates
-----------------------------------------

*   **Metric tensor:**
    
    \[latex\]\\eqalign{ \\left\\{ \\begin{aligned} g\_{ij}=\\vec{a}\_i\\cdot \\vec{a}\_j \\qquad\\qquad\\qquad\\quad\\\\ det\[g\_{ij}\]=det\[\\vec{a}\_i\]det\[\\vec{a}\_j\]=J^2 \\end{aligned} \\right. }\[/latex\]
    
*   **Inverse metric tensor**:
    
    \[latex\]\\eqalign{ \\left\\{ \\begin{aligned} g^{ij}, \\quad \\vec{a}^i\\cdot \\vec{a}^j \\qquad\\qquad\\qquad\\quad\\\\ det\[g^{ij}\]=det\[\\vec{a}^i\]det\[\\vec{a}^j\]=\\frac{1}{J^2} \\end{aligned} \\right. }\[/latex\]
    
*   **Identity tensor:**
    
    \[latex\]\\eqalign{ \\overline{\\overline I} =I^{ij}\\vec{a\_i}\\vec{a\_j}=I\_{ij}\\vec{a^i}\\vec{a^j}=I^{i}\_{\\bullet j}\\ \\vec{a\_i}\\vec{a^j}=I^{\\bullet j}\_{i}\\ \\vec{a^i}\\vec{a\_j} }\[/latex\]
    
    **Matrix operation with identity tensor**
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-1.png)
    
*   **Inverse metric tensor and Metric tensor**:
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-2.png)
    

* * *

Associated Tensors
------------------

The associated tensors can be obtained by raising or lowering of indices (using identity matrix)

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-3.png)