---
title: '[Lecture Notes] Advanced Computation Methods for Fluid Flow – 06'
tags:
  - Advanced Computation Methods for Fluid Flow - 2018
  - computational fluid dynamics
  - numerical method
id: '589'
date: 2018-04-14 12:47:18
---

> _28/03/2018, Chapter2 - General Curvilinear Coordinates_

* * *

General Tensor Transformation Rule
----------------------------------

### Coordinate Transformation

With a given frame, vectors and tensors are unware of the bases we choose to represent them. The change of basis \[latex\](\\xi^1, \\ \\xi^2,\\ \\xi^3)\\rightarrow(\\overline{\\xi}^1, \\ \\overline{\\xi}^2,\\ \\overline{\\xi}^3)\[/latex\] on thes same vector \[latex\]d\\vec{r} \\ (d\\underline{\\vec{r}})\[/latex\] is shown in the following Figure.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-4.png)

### Tensor Transformation Rule

Consider two general curvilinear coordinates \[latex\](\\xi^1, \\ \\xi^2,\\ \\xi^3)\\ \\& \\ (\\overline{\\xi}^1, \\ \\overline{\\xi}^2,\\ \\overline{\\xi}^3)\[/latex\], chain rule of transformation for **covariant base vectors** between two coordinates are

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} \\underline{\\vec{a}}\_j=\\frac{\\partial \\underline{\\vec{r}}}{\\partial \\overline{\\xi}^j} =\\frac{\\partial \\vec{r}}{\\partial \\overline{\\xi}^j}= \\frac{\\partial \\vec{r}}{\\partial \\xi^i}\\frac{\\partial \\xi^i}{\\partial \\overline{\\xi}^j}=\\quad C^i\_j\\vec{a}\_i\\\\ \\vec{a}\_j=\\frac{\\partial \\vec{r}}{\\partial \\xi^j} =\\frac{\\partial \\underline{\\vec{r}}}{\\partial \\xi^j}= \\frac{\\partial \\underline{\\vec{r}}}{\\partial \\overline{\\xi}^i}\\frac{\\partial \\overline{\\xi}^i}{\\partial \\xi^j}=(C^{-1})^i\_j\\underline{\\vec{a}}\_i \\end{aligned} \\right. }\[/latex\]

In similar way, the transformation for contravariant base vectors are

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} \\vec{a}^i=\\ C^i\_j\\ \\underline{\\vec{a}}^j\\\\ \\underline{\\vec{a}}^i=(C^{-1})^i\_j\\ \\vec{a}^j \\end{aligned} \\right. }\[/latex\]

### Jacobian of Transformation

The Jacobian of transformation between two coordinate is define as

\[latex\]\\eqalign{ J\_t=\\frac{\\partial (\\xi^1, \\xi^2 ,...,\\xi^n)}{\\partial(\\overline{\\xi}^1,\\overline{\\xi}^2,...,\\overline{\\xi}^n)}=\\begin{vmatrix} \\frac{\\partial \\xi}{\\partial \\overline{\\xi}} \\end{vmatrix} }\[/latex\]

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-5.png)

And \[latex\]J\_t, J, \\overline{J}\[/latex\] has the following relationship

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-6.png)

* * *

General Tensor Transformation
-----------------------------

Then, the general transformation formulation for any Tensor between two coordinates can be derived as

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-7.png)

Here, we introduce some examples of tensor transformation.

### Transformation: base vectors, reciprocal base vectors

As descriptions above, the base vectors and reciprocal base vectors can be transfered between two coordinates.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-8.png)

### Transformation: contravariant components, covariant components

Both the base vectors and their components satisfy the general tensor transformation rule.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-9.png)

### Transformation: covariant permutation tensor, covariant alternating tensor

*   **covariant permutation tensor**
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-10.png)
    
*   **covariant alternating tensor**
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-11.png)
    

### Transformation: convariant permutation tensor, convariant alternating tensor

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-12.png)