---
title: '[Lecture Notes] Advanced Computation Methods for Fluid Flow  - 04'
tags:
  - Advanced Computation Methods for Fluid Flow - 2018
  - computational fluid dynamics
  - numerical method
id: '454'
date: 2018-03-29 00:10:47
---

> _21/03/2018, Chapter2 - General Curvilinear Coordinates_

* * *

Covariant and Contravariant Basis
---------------------------------

The covariant and contravariant base vectors have been presented in [note 3](https://bhlin.co.network/wp/2018/03/27/lecture-notes-advanced-computation-methods-for-fluid-flow-03/).

![Alt text](https://bhlin.co.network/wp/wp-content/uploads/2018/03/未命名-4.png)

*   **Covariant basis (contravariant components)**
    
    \[latex\]\\eqalign{ \\vec{A} =A^i\\vec{a\_i}= A^1 \\vec{a\_1}+ A^2 \\vec{a\_2}+ A^3 \\vec{a\_3} \\\\ \\vec{a\_i}: \\textrm{covariant base vector} }\[/latex\]
    
    In the coordinate direction.
    
*   **Contravariant basis (covariant components)**
    
    \[latex\]\\eqalign{ \\vec{A} =A\_i\\vec{a^i}= A\_1 \\vec{a^1}+ A\_2 \\vec{a^2}+ A\_3 \\vec{a^3} \\\\ \\vec{a^i}: \\textrm{contravariant base vector} }\[/latex\]
    
    Prependicular to coordinate surface. **Note!** The vector \[latex\]\\vec{A} \[/latex\] itself is coordinate invariant, but may be decomposed into different components using different bases.
    
*   **Important to remember !**
    
    1.  \[latex\]\\vec{a\_i}, \\vec{a^i} \[/latex\] need **not be of unit length**.
    2.  \[latex\]\\vec{A} \\cdot \\vec{a^i} \[/latex\] is the contravariant component in \[latex\]\\vec{a\_i}\[/latex\] direction.
    3.  \[latex\]\\vec{A} \\cdot \\vec{a^i} \[/latex\] does **not** represent the projection of \[latex\]\\vec{A}\[/latex\] in \[latex\]\\vec{a^i}\[/latex\] direction.

* * *

Tensor Components in Curilinear Coordinate
------------------------------------------

*   **Second-order tensors** Stress, rate of strain, velocity gradient, etc. are second-order tensor.
    
    \[latex\]\\eqalign{ \\overline{\\overline T} = T^{ij}\\vec{a\_i}\\vec{a\_j}=\\quad \\quad \\quad\\\\ T^{11}\\vec{a}\_1\\vec{a}\_1+T^{12}\\vec{a}\_1\\vec{a}\_2+T^{13}\\vec{a}\_1\\vec{a}\_3\\\\+ T^{21}\\vec{a}\_2\\vec{a}\_1+T^{22}\\vec{a}\_2\\vec{a}\_2+T^{23}\\vec{a}\_2\\vec{a}\_3\\\\+ T^{31}\\vec{a}\_3\\vec{a}\_1+T^{32}\\vec{a}\_3\\vec{a}\_2+T^{33}\\vec{a}\_3\\vec{a}\_3\\\\ }\[/latex\]
    
    In general, \[latex\]T^{ij}\\neq T^{ji}\[/latex\] for curvilinear coordinates.
    
*   **Four different coordinate bases**
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/03/未命名2-1.png)
    

* * *

Tensor Analysis for Fluid Flows
-------------------------------

*   Scalar (\[latex\]0^th - order\[/latex\]): \[latex\]\\phi=p,T,\\rho,\\mu,C,...\[/latex\]
    
*   Vector (\[latex\]1^th - order\[/latex\]): \[latex\]\\vec{A}=A^i\\vec{a\_i},...\[/latex\]
    
*   \[latex\]2^th - order \\ tensor\[/latex\]: \[latex\]\\overline{\\overline T} =T^{ij}\\vec{a\_i}\\vec{a\_j}=...,\\\\ \\sigma^{ij},... \[/latex\]
    
*   \[latex\]3^th - order \\ tensor\[/latex\]: \[latex\]\\overline{\\overline{\\overline U}} =U^{ijK}\\vec{a\_i}\\vec{a\_j}\\vec{a\_k},...\[/latex\]
    

* * *

Stress Tensor!
--------------

![](https://bhlin.co.network/wp/wp-content/uploads/2018/03/未命名-5.png)

![](https://bhlin.co.network/wp/wp-content/uploads/2018/03/未命名2.png)