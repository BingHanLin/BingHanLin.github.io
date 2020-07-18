---
title: '[Lecture Notes] Advanced Computation Methods for Fluid Flow  - 03'
tags:
  - Advanced Computation Methods for Fluid Flow - 2018
  - computational fluid dynamics
  - numerical method
id: '364'
date: 2018-03-28 00:41:26
---

> _21/03/2018, Chapter2 - General Curvilinear Coordinates_

* * *

Coordinate Basis
----------------

The equations for conservation laws have been derived in [previous note](https://bhlin.co.network/wp/2018/03/22/lecture-notes-advanced-computation-methods-for-fluid-flow-02/). These equations are written in coordinate-free form, while they can be solved by numerical computation only if they are expressed in component forms. Thus, this requires us to introduce a coordinate basis. The selection of coordinate basis is dictated by the geometry and boundary conditions of the physical problem. Some coordinate basis are list in the following table.

Name

Coordinates

Basis

Cartesian basis

\[latex\](x, y, z)\[/latex\]

\[latex\](\\hat{i}, \\hat{j}, \\hat{k})\[/latex\]

Cylindrical basis

\[latex\](x, r, \\theta)\[/latex\]

\[latex\](\\hat{e\_x}, \\hat{e\_r}, \\hat{e\_\\theta})\[/latex\]

Spherical basis

\[latex\](r, \\theta, \\phi)\[/latex\]

\[latex\](\\hat{e\_r}, \\hat{e\_\\theta}, \\hat{e\_\\phi})\[/latex\]

Orthogonal Curvilinear basis

\[latex\](x^1, x^2, x^3)\[/latex\]

\[latex\](\\hat{e\_1}, \\hat{e\_2}, \\hat{e\_3})\[/latex\]

General Curvilinear basis

\[latex\](\\xi^2, \\xi^2, \\xi^3)\[/latex\]

\[latex\](\\vec{a\_1}, \\vec{a\_2}, \\vec{a\_3})\[/latex\]

Here, we choose the most general basis, **non-orthogonal cuvilinear basis**, as our coordinate basis. One thing to be noted, \[latex\]\\vec{a\_i}\[/latex\] need not to be the unit vector.

![Alt text](https://bhlin.co.network/wp/wp-content/uploads/2018/03/未命名.jpg)

* * *

Tensor Analysis (covariant base vectors)
----------------------------------------

*   **General basis**
    
    ![Alt text](https://bhlin.co.network/wp/wp-content/uploads/2018/03/%E6%9C%AA%E5%91%BD%E5%90%8D-1.png)
    
    Non-orthogonal cuvilinear basis is defined by any fixed set of "non-coplannar vectors" \[latex\]\\left\\{\\vec{a\_i} \\right\\} = \\left\\{\\vec{a\_1}, \\vec{a\_2}, \\vec{a\_3} \\right\\}\[/latex\] which are also called **covariant base vectors**. Any vector \[latex\]\\vec{A}\[/latex\] in the space can be uniquely represented by
    
    \[latex\]\\eqalign{ \\vec{A} = A^1 \\vec{a\_1}+ A^2 \\vec{a\_2}+ A^3 \\vec{a\_3} = \\sum\_{i=1}^3 A^i \\vec{a\_i} \\\\ = A^i \\vec{a\_i} = A^j \\vec{a\_j} = A^n \\vec{a\_n} }\[/latex\]
    
    Each base vector has three components, thus
    
    \[latex\]\\eqalign{ \\overline{\\overline A} = \\left\[a^j\_i\\right\]=\\left\[\\vec{a\_i}\\right\] =\\begin{bmatrix}a^1\_1 & a^2\_1 & a^3\_1\\\\ a^1\_2 & a^2\_2 & a^3\_2\\\\ a^1\_3 & a^2\_3 & a^3\_3 \\end{bmatrix} }.\[/latex\]
    
*   **Jacobian of a basis**
    
    ![Alt text](https://bhlin.co.network/wp/wp-content/uploads/2018/03/%E6%9C%AA%E5%91%BD%E5%90%8D-2-300x153.png)
    
    Jacobian \[latex\]J\[/latex\] is the volume enclosed by base vectors
    
    \[latex\]\\eqalign{ J =\\left( \\vec{a\_1}\\times\\vec{a\_2}\\right) \\cdot\\vec{a\_3} \\quad = \\quad \\mid \\vec{a\_1}\\times\\vec{a\_2} \\mid \\mid \\vec{a\_3} \\mid \\cos\\alpha \\quad = \\quad \\mid \\vec{a\_1}\\mid \\mid \\vec{a\_2} \\mid \\mid \\vec{a\_3} \\mid \\sin\\theta \\cos\\alpha .}\[/latex\]
    
    Because of non-coplannar vectors \[latex\]\\vec{a\_i}\[/latex\] are non-coplannar, \[latex\]J\\neq 0\[/latex\]. Volume is positive for the cyclic order of \[latex\] \\left(1, 2, 3 \\right) \[/latex\].
    
*   **Permutation Tensor** The covariant components of a permutation tensor \[latex\]e\_{ijk}\[/latex\] can be expressed as
    
    \[latex\]\\eqalign{ e\_{ijk} \\quad = \\quad\\vec{a\_i} \\cdot\\left( \\vec{a\_j}\\times\\vec{a\_k}\\right) }\[/latex\]
    
    and
    
    \[latex\]\\eqalign{ e\_{ijk} =\\left\\{ \\begin{aligned} J, \\quad \\textrm{if (ijk) is an even permutation of (123)} \\\\ -J, \\quad \\textrm{if (ijk) is an odd permutation of (123)} \\\\ 0, \\quad \\textrm{if any two indices are equal (coplannar)} \\end{aligned} \\right. .}\[/latex\]
    
    The determinant of the permutation tensor is
    
    \[latex\]\\eqalign{ e\_{ijk} \\quad = \\quad\\vec{a\_i} \\cdot\\left( \\vec{a\_j}\\times\\vec{a\_k}\\right) = \\begin{vmatrix}a^1\_i & a^2\_i & a^3\_i\\\\ a^1\_j & a^2\_j & a^3\_j\\\\ a^1\_k & a^2\_k & a^3\_k \\end{vmatrix} .}\[/latex\]
    
*   **Alternating Tensor** The covariant components of an alternating tnesor \[latex\]\\xi\_{ijk}\[/latex\] an be
    
    \[latex\]\\eqalign{ \\xi\_{ijk} \\quad = \\frac{e\_{ijk}}{J}\\quad = \\quad \\frac{1}{J}\\ \\vec{a\_i} \\cdot\\left( \\vec{a\_j}\\times\\vec{a\_k}\\right) }\[/latex\]
    
    and
    
    \[latex\]\\eqalign{ \\xi\_{ijk} =\\left\\{ \\begin{aligned} 1, \\quad \\textrm{if (ijk) is an even permutation of (123)} \\\\ -1, \\quad \\textrm{if (ijk) is an odd permutation of (123)} \\\\ 0, \\quad \\textrm{if any two indices are equal (coplannar)} \\end{aligned} \\right. }\[/latex\]
    

* * *

Tensor Analysis (contravariant base vectors)
--------------------------------------------

*   **Contraviariant Base Vectors** Contraviariant Base Vectors are representations of the same vector using the **reciprocal basis**. They are defined as
    
    \[latex\]\\eqalign{ \\vec{a^i} \\quad = \\quad \\frac{1}{J}\\left( \\vec{a\_j}\\times\\vec{a\_k}\\right) }\[/latex\]
    
    where \[latex\]ijk\[/latex\] is in cyclic order. Covariant and contravariant base vectors are **mutually prependicular**.
    
    ![Alt text](https://bhlin.co.network/wp/wp-content/uploads/2018/03/未命名-3.png)
    
    Hence, covariant and contravariant base vectors have the following features
    
    \[latex\]\\eqalign{ \\vec{a^i} \\cdot \\vec{a\_m} = \\ \\frac{1}{J}\\left( \\vec{a\_j}\\times\\vec{a\_k}\\right)\\cdot \\vec{a\_m}\\\\= \\frac{1}{J} e\_{mjk}=\\xi\_{mjk}=\\left\\{ \\begin{aligned} 1, \\textrm{if}\\quad m=i\\\\ 0,\\textrm{if} \\quad m\\neq i \\end{aligned} =\\delta^i\_m \\right. }\[/latex\]
    
    and
    
    \[latex\]\\eqalign{ \\left\\{ \\begin{aligned} \\vec{a^1} \\cdot \\vec{a\_2}=\\vec{a^1} \\cdot \\vec{a\_3}=0\\\\ \\vec{a^2} \\cdot \\vec{a\_1}=\\vec{a^2} \\cdot \\vec{a\_3}=0\\\\ \\vec{a^3} \\cdot \\vec{a\_1}=\\vec{a^3} \\cdot \\vec{a\_2}=0\\\\ \\vec{a^1} \\cdot \\vec{a\_1}=\\vec{a^2} \\cdot \\vec{a\_2}=\\vec{a^3} \\cdot \\vec{a\_3}=1\\\\ \\end{aligned} \\right. }\[/latex\]
    
    **Note!** \[latex\]\\vec{a^i}\[/latex\] is prependucular to both \[latex\]\\vec{a\_j}\[/latex\] and \[latex\]\\vec{a\_k}\[/latex\] but \[latex\]\\vec{a^i}\[/latex\], in general, is not parallel to \[latex\]\\vec{a^i}\[/latex\]. That is,
    
    \[latex\]\\eqalign{ \\vec{a^1} \\cdot \\vec{a\_1}=1= \\mid\\vec{a^1}\\mid\\mid\\vec{a\_1}\\mid \\cos \\beta=1\\\\ but \\quad \\mid\\vec{a^1}\\mid \\neq \\mid\\vec{a\_1}\\mid \\neq1 \\quad \\left(\\beta \\neq 0^o\\right) .}\[/latex\]
    
    Also, we define a new tensor for contraviariant Base
    
    \[latex\]\\eqalign{ \\overline{\\overline \\alpha} = \\left\[\\alpha^j\_i\\right\]=\\left\[\\vec{a^i}\\right\] = \\left\[\\vec{a^1},\\vec{a^2},\\vec{a^3}\\right\] =\\begin{bmatrix}\\alpha^1\_1 & \\alpha^2\_1 & \\alpha^3\_1\\\\ \\alpha^1\_2 & \\alpha^2\_2 & \\alpha^3\_2\\\\ \\alpha^1\_3 & \\alpha^2\_3 & \\alpha^3\_3 \\end{bmatrix} }.\[/latex\]
    
*   **Permutation Tensor** The contravariant components of a permutation tensor \[latex\]e^{ijk}\[/latex\] can be expressed as
    
    \[latex\]\\eqalign{ e^{ijk} \\quad = \\quad\\vec{a^i} \\cdot\\left( \\vec{a^j}\\times\\vec{a^k}\\right) }\[/latex\]
    
    and
    
    \[latex\]\\eqalign{ e^{ijk} =\\left\\{ \\begin{aligned} J, \\quad \\textrm{if (ijk) is an even permutation of (123)} \\\\ -J, \\quad \\textrm{if (ijk) is an odd permutation of (123)} \\\\ 0, \\quad \\textrm{if any two indices are equal (coplannar)} \\end{aligned} \\right. .}\[/latex\]
    
    \[latex\]\\frac{1}{J}\[/latex\] is the volume enclosed by \[latex\]\\left(\\vec{a^i},\\vec{a^j},\\vec{a^k}\\right)\[/latex\].The determinant of the permutation tensor is
    
    \[latex\]\\eqalign{ e^{ijk} \\quad = \\quad\\vec{a^i} \\cdot\\left( \\vec{a^j}\\times\\vec{a^k}\\right) = \\begin{vmatrix}\\alpha^i\_1 & \\alpha^j\_1 & \\alpha^k\_1\\\\ \\alpha^i\_2 & \\alpha^j\_2 & \\alpha^k\_2\\\\ \\alpha^i\_3 & \\alpha^j\_3 & \\alpha^k\_3 \\end{vmatrix} .}\[/latex\]
    
*   **Alternating Tensor** The contravariant components of an alternating tnesor \[latex\]\\xi^{ijk}\[/latex\] an be
    
    \[latex\]\\eqalign{ \\xi^{ijk} \\quad = \\quad Je\_{ijk}\\quad = \\quad J\\ \\vec{a^i} \\cdot\\left( \\vec{a^j}\\times\\vec{a^k}\\right) }\[/latex\]
    
    and
    
    \[latex\]\\eqalign{ \\xi^{ijk} =\\left\\{ \\begin{aligned} 1, \\quad \\textrm{if (ijk) is an even permutation of (123)} \\\\ -1, \\quad \\textrm{if (ijk) is an odd permutation of (123)} \\\\ 0, \\quad \\textrm{if any two indices are equal (coplannar)} \\end{aligned} \\right. }\[/latex\]
    
*   **Some useful tensor operations**
    

1.  \[latex\]\\eqalign{ e^{ijk} e\_{lmn}=\\begin{bmatrix}\\vec{a^i} \\\\\\vec{a^j} \\\\\\vec{a^k} \\end{bmatrix}\\cdot \\begin{bmatrix}\\vec{a\_l} &\\vec{a\_m} &\\vec{a\_n} \\end{bmatrix} \\\\= \\begin{bmatrix}\\vec{a^i}\\cdot \\vec{a\_l} & \\vec{a^i}\\cdot \\vec{a\_m}&\\vec{a^i}\\cdot \\vec{a\_n} \\\\ \\vec{a^j}\\cdot \\vec{a\_l} & \\vec{a^j}\\cdot \\vec{a\_m}&\\vec{a^j}\\cdot \\vec{a\_n} \\\\ \\vec{a^k}\\cdot \\vec{a\_l} & \\vec{a^k}\\cdot \\vec{a\_m}&\\vec{a^k}\\cdot \\vec{a\_n} \\end{bmatrix}=\\begin{bmatrix} \\delta^i\_j & \\delta^i\_m &\\delta^i\_n \\\\ \\delta^j\_j & \\delta^j\_m &\\delta^j\_n \\\\ \\delta^k\_j & \\delta^k\_m &\\delta^k\_n \\end{bmatrix} }\[/latex\]
    
2.  \[latex\]e^{ijk} e\_{imn}=\\delta^j\_m\\delta^k\_n-\\delta^j\_n\\delta^k\_m\[/latex\] (sum over i, 81 terms)
    
3.  \[latex\]e^{ijk} e\_{ijn}=\\delta^j\_j\\delta^k\_n-\\delta^j\_n\\delta^k\_j=2\\delta^k\_n\[/latex\] (sum over i, j)