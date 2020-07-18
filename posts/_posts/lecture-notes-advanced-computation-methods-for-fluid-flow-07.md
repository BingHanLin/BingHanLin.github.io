---
title: '[Lecture Notes] Advanced Computation Methods for Fluid Flow – 07'
tags:
  - Advanced Computation Methods for Fluid Flow - 2018
  - computational fluid dynamics
  - numerical method
id: '640'
date: 2018-05-01 22:44:22
---

> _11/04/2018, Chapter2 - General Curvilinear Coordinates_

* * *

Differentiation of Tensors: Covariant Derivatives
-------------------------------------------------

*   **Purpose:**

1.  Define a derivative which preserves tensor characteristics and reduces to the familiar partial derivatives in Cartesian coordinate.
    
2.  Define a **covariant derivative** of tensors similar to partial derivatives as follow.
    
    \[latex\]\\eqalign{ (A+B),\_i =A,\_i+B,\_i \\\\ (AB),\_i =A,\_iB+AB,\_i \\\\ dA = A(\\xi^i+d\\xi^i)-A(\\xi^i) = A,\_id\\xi^i }\[/latex\]
    

* * *

Partial Derivative of Scalar
----------------------------

*   **First Derivative**
    
    \[latex\]\\eqalign{ \\overline{D}\_i=\\frac{\\partial \\phi}{\\partial \\xi^i}=\\frac{\\partial \\phi}{\\partial \\xi^k}\\frac{\\partial \\xi^k}{\\partial \\bar{\\xi}^i}=D\_k(\\frac{\\partial \\xi^k}{\\partial \\bar{\\xi}^i}) }\[/latex\]
    
    Satisfies the tensor transformation rule.
    
*   **Second Derivatives**
    
    \[latex\]\\eqalign{ \\overline{D}\_{ij}=D\_{mn}\\left(\\frac{\\partial \\xi^m}{\\partial \\bar{\\xi}^i}\\frac{\\partial \\xi^n}{\\partial \\bar{\\xi}^j}\\right)+D\_{m}\\left(\\frac{\\partial^2 \\xi^m}{\\partial \\bar{\\xi}^i\\partial \\bar{\\xi}^j }\\right) }\[/latex\]
    
    Doesn't satisfy the tensor transformation rule.
    

> In Curvilinear Coordinates the first derivative is a tensor, but the second and higher derivatives are **NOT** tensors.

* * *

Partial Derivative of Vectors
-----------------------------

\[latex\]\\eqalign{ \\frac{\\partial \\vec{A}}{\\partial \\xi^j} = \\frac{\\partial}{\\partial \\xi^j}(A^i\\vec{a}\_i)=\\frac{\\partial A^i}{\\partial \\xi^j}\\vec{a}\_i+A^i\\frac{\\partial \\vec{a}\_i}{\\partial \\xi^j} }\[/latex\]

Need to evaluate the derivative of base vectors for general curvilinear coordinate systems. Thus, we introduce Christoffel Symbols.

* * *

Christoffel Symbols
-------------------

Christoffel symbols represents the rate of change of \[latex\]i^{th}\[/latex\] base vector with respect to the \[latex\]j^{th}\[/latex\]-coordinate, resolved along the \[latex\]k^{th}\[/latex\]-coordinate direction.

\[latex\]\\eqalign{ \\frac{\\partial \\vec{a}\_i}{\\partial \\xi^j} = \\Gamma^k\_{ij}\\vec{a}\_k }\[/latex\]

* * *

Covariant Derivative of Base Vectors
------------------------------------

With Christoffel Symbols, let's define covariant derivative of base vectors:

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} \\vec{a}\_{i,j}=\\frac{\\partial \\vec{a}\_i}{\\partial \\xi^j}-\\Gamma^k\_{ij}\\vec{a}\_k=0 \\quad(but \\ \\frac{\\partial \\vec{a}\_i}{\\partial \\xi^j}\\neq0, \\ \\Gamma^k\_{ij} \\neq0) \\\\ \\vec{a}^i\_{,j}=\\frac{\\partial \\vec{a}^i}{\\partial \\xi^j}-\\Gamma^i\_{kj}\\vec{a}^k=0 \\quad(but \\ \\frac{\\partial \\vec{a}^i}{\\partial \\xi^j}\\neq0, \\ \\Gamma^i\_{kj} \\neq0) \\end{aligned} \\right. }\[/latex\]

The **base vectors and reciprocal base vectors are covariantly invariant**. Therefore, the covariant derivatives in a general basis are the same as partial derivatives in the Cartesian basis (for absolute tensors).

* * *

Covariant Derivative of Vectors
-------------------------------

With the similar operation with [partial derivative of vectors](#Partial_Derivative_of_Vectors) but we take Christoffel symbol into the equation.

\[latex\]\\eqalign{ \\begin{align} \\frac{\\partial \\vec{A}}{\\partial \\xi^j} &= \\frac{\\partial A^i}{\\partial \\xi^j}\\vec{a}\_i+A^i\\frac{\\partial \\vec{a}\_i}{\\partial \\xi^j}\\\\ &=\\frac{\\partial A^i}{\\partial \\xi^j}\\vec{a}\_i+A^i\\Gamma^k\_{ij}\\vec{a}\_k =\\frac{\\partial A^i}{\\partial \\xi^j}\\vec{a}\_i+A^k\\Gamma^i\_{kj}\\vec{a}\_i= \\left( \\frac{\\partial A^i}{\\partial \\xi^j}+A^k\\Gamma^i\_{kj} \\right)\\vec{a}\_i \\\\ &=A^i\_{,j}\\vec{a}\_i = (A^i\\vec{a}\_i)\_{,j}=\\vec{A}\_{,j} \\end{align} }\[/latex\]

From the derivation above, we obtain covariant derivative of vectors \[latex\]\\vec{A}\_{,j}\[/latex\] which has the same meaning as partial derivative but contain Christoffel symbol in its operation.

* * *

Covariant Derivative of Second-Order Tensors
--------------------------------------------

Next, we present the covariant derivative of second-order tensors.

\[latex\]\\eqalign{ \\begin{align} \\frac{\\partial \\overline{\\overline{T}}}{\\partial \\xi^m} &=\\frac{\\partial}{\\partial \\xi^m}\\left(T^{ij}\\vec{a}\_i\\vec{a}\_j\\right)=\\frac{\\partial T^{ij}}{\\partial \\xi^m}\\vec{a}\_i\\vec{a}\_j+T^{ij}\\left(\\frac{\\partial \\vec{a}\_i}{\\partial \\xi^m}\\vec{a}\_j + \\vec{a}\_i\\frac{\\partial \\vec{a}\_j}{\\partial \\xi^m}\\right)\\\\ &=\\frac{\\partial T^{ij}}{\\partial \\xi^m}\\vec{a}\_i\\vec{a}\_j + T^{ij}\\left(\\Gamma^n\_{im}\\vec{a}\_n\\vec{a}\_j + \\vec{a}\_i\\Gamma^n\_{jm}\\vec{a}\_n\\right)\\\\ &=\\frac{\\partial T^{ij}}{\\partial \\xi^m}\\vec{a}\_i\\vec{a}\_j + \\left(T^{nj}\\Gamma^i\_{nm}\\vec{a}\_i\\vec{a}\_j + T^{in}\\Gamma^j\_{nm}\\vec{a}\_i\\vec{a}\_j\\right)\\\\ &=\\left( \\frac{\\partial T^{ij}}{\\partial \\xi^m}+T^{nj}\\Gamma^i\_{nm}+ T^{in}\\Gamma^j\_{nm} \\right)\\vec{a}\_i\\vec{a}\_j\\\\ &=T^{ij}\_{,m}\\vec{a}\_i\\vec{a}\_j =(T^{ij}\\vec{a}\_i\\vec{a}\_j )\_{,m}=\\overline{\\overline{T}}\_{,m} \\end{align} }\[/latex\]

* * *

Covariant Derivative for a General Teonsors of Weight \[latex\]w\[/latex\]
--------------------------------------------------------------------------

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/擷取.png) ![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/擷取2.png)

* * *

Computation of Christoffel Symbols
----------------------------------

> Christoffel symbols are **not** tensors, and they do not follow tensor transforamtion rule under coordinate transformation.

Here we show some ways to compute the Christoffel symbols.

### Method 1.

\[latex\]\\eqalign{ \\Gamma^i\_{jk} = \\frac{1}{2}g^{ij}\\left( \\frac{\\partial g\_{ij}}{\\partial \\xi^k}+\\frac{\\partial g\_{kl}}{\\partial \\xi^j}+\\frac{\\partial g\_{jk}}{\\partial \\xi^l} \\right)=\\Gamma^i\_{kj} }\[/latex\]

with the derivation as follow

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/擷取3.png)

### Method 2.

\[latex\]\\eqalign{ \\vec{a}^i \\cdot \\frac{\\partial \\vec{a}\_j}{\\partial \\xi^k}=\\vec{a}^i \\cdot(\\Gamma^l\_{jk}\\vec{a}\_l)=\\delta^i\_l\\Gamma^l\_{jk}=\\Gamma^i\_{jk} }\[/latex\]

where \[latex\] \\Gamma^i\_{jk} \[/latex\] is the \[latex\] i^{th} \[/latex\] component of the derivative of \[latex\] \\vec{a}\_j \[/latex\] with repect to \[latex\] \\xi^k \[/latex\]

### Contraction of Christoffel Symbols

\[latex\]\\eqalign{ \\Gamma^i\_{ij}=\\Gamma^i\_{ji}=\\frac{1}{J}\\frac{\\partial J}{\\partial \\xi^j} \\qquad (=\\Gamma^1\_{1j}+\\Gamma^2\_{2j}+\\Gamma^3\_{3j}) }\[/latex\]

with the derivation as follow

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/擷取4.png)

* * *

Vector Operations in Tensor Form
--------------------------------

*   **Gradient**
    
    \[latex\]\\eqalign{ \\nabla \\phi=\\vec{a}^i(\\phi)\_{,i}=\\vec{a}^i\\frac{\\partial \\phi}{\\partial \\xi^i}=\\frac{\\partial \\phi}{\\partial \\xi^i}g^{ij}\\vec{a}\_j=\\frac{\\partial \\phi}{\\partial \\xi^j}g^{ji}\\vec{a}\_i }\[/latex\]
    
*   **Divergence**
    
    \[latex\]\\eqalign{ \\nabla \\cdot \\vec{A}=\\vec{a}^i\\cdot(\\vec{A})\_{,i}=\\vec{a}^i\\cdot(A^j\\vec{a}\_j)\_{,i}=A^j\_{,i}(\\vec{a}^i \\cdot \\vec{a}\_j) = A^j\_{,i}\\delta^i\_j=A^i\_{,i} }\[/latex\]
    
*   **Curl**
    
    \[latex\]\\eqalign{ \\nabla \\times \\vec{A}=\\vec{a}^i\\times(\\vec{A})\_{,i}=\\vec{a}^i\\times(A\_j\\vec{a}^j)\_{,i}=A\_{j,i}(\\vec{a}^i \\times \\vec{a}^j) \\\\= A\_{j,i}e^{ijk}\\vec{a}\_k=-A\_{i,j}e^{ijk}\\vec{a}\_k= e^{ijk}g\_{jm}A^m\_{,i}\\vec{a}\_k }\[/latex\]
    
*   **Outer Product**
    
    \[latex\]\\eqalign{ \\nabla \\vec{A}=\\vec{a}^i(\\vec{A})\_{,i}=\\vec{a}^i(A^j\\vec{a}\_j)\_{,i}=A^j\_{,i}(\\vec{a}^i \\vec{a}\_j) \\\\ = g^{ik} A^j\_{,i}\\vec{a}\_k\\vec{a}\_j= g^{ik} A^j\_{,k}\\vec{a}\_i\\vec{a}\_j }\[/latex\]
    
*   **Laplacian of a scalar**
    
    \[latex\]\\eqalign{ \\nabla^2 \\phi=\\nabla\\cdot(\\nabla\\phi)=\\vec{a}^i\\cdot(\\vec{a}^j\\phi\_{,j})\_{,i}=\\vec{a}^i\\cdot\\vec{a}^j\\phi\_{,ji}=g^{ij}\\phi\_{,ij} }\[/latex\]
    
*   **Laplacian of a vector**
    
    \[latex\]\\eqalign{ \\begin{align} \\nabla^2 \\vec{A}&=\\nabla\\cdot(\\nabla\\vec{A})\\\\ &=\\vec{a}^k\\cdot\[\\vec{a}^j(A^i\\vec{a}\_i)\_{,j}\]\_{,k}=(\\vec{a}^k\\cdot\\vec{a}^j)(A^i\_{,j}\\vec{a}\_i)\_{,k}=g^{jk}A^i\_{,jk}\\vec{a}\_i \\end{align} }\[/latex\]