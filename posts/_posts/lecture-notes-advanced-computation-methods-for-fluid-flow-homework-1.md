---
title: '[Lecture Notes] Advanced Computation Methods for Fluid Flow – Homework 1'
tags:
  - Advanced Computation Methods for Fluid Flow - 2018
  - computational fluid dynamics
  - numerical method
id: '529'
date: 2018-04-09 15:57:17
---

> _08/04/2018, Homework No. 1_

* * *

Question 1
----------

1.  Given covariant base vectors \[latex\]\\vec{a}\_1=(0.2,0.3,0.1), \[/latex\] \[latex\]\\vec{a}\_2=(0.4,-0.2,0.1),\[/latex\] \[latex\]\\vec{a}\_3=(0.1,-0.6,-0.2)\[/latex\].
    *   (a) Calculate the determinant \[latex\]J\[/latex\] of \[latex\]\\left\[\\vec{a}\_i\\right\]\[/latex\]
    *   (b) Find the reciprocal (contravariant) base vectors \[latex\]\\vec{a}^i\[/latex\]
    *   (c) Calculate \[latex\]\\vec{a}^i \\cdot \\vec{a}\_j\\ (i,j=1,2,3)\[/latex\] and verify that \[latex\]\\vec{a}^i \\cdot \\vec{a}\_j=\\delta^i\_j\[/latex\].
    *   (d) Calculate the determinant \[latex\]J^\*\[/latex\] of \[latex\]\\vec{a}^i\[/latex\], and show that \[latex\]J^\* =\\frac{1}{J}\[/latex\].
    *   (e) Find the contravariant (\[latex\]v^i\[/latex\]) and covariant (\[latex\]v\_i\[/latex\]) components of the velocity vector \[latex\]\\vec{V}=(1,-3,1.5)\[/latex\].

### Answer 1.a

Take cyclic order of (1,2,3).

\[latex\]\\eqalign{ J= \\vec{a}\_1 \\cdot (\\vec{a}\_2 \\times \\vec{a}\_3) = \\begin{vmatrix}a^1\_1 & a^2\_1 & a^3\_1\\\\ a^1\_2 & a^2\_2 & a^3\_2\\\\ a^3\_k & a^2\_3 & a^3\_3 \\end{vmatrix} = \\begin{vmatrix}0.2 & 0.3 & 0.1\\\\ 0.4 & -0.2 & 0.1\\\\ 0.1 & -0.6 & -0.2 \\end{vmatrix} }\[/latex\]

After the calculations, the solution is obtained.

\[latex\]\\eqalign{ J= 0.008+0.003-0.024+0.002+0.012+0.024= 0.025 }\[/latex\].

### Answer 1.b

In cyclic order,

\[latex\]\\eqalign{ \\vec{a}^i= \\frac{1}{J} \\vec{a}\_j\\times \\vec{a}\_k. }\[/latex\]

Calculate \[latex\]\\vec{a}^1, \\vec{a}^2, \\vec{a}^3\[/latex\] from above formulation, we have

\[latex\]\\eqalign{ \\vec{a}^1= \\frac{1}{J} \\vec{a}\_2\\times \\vec{a}\_3=\\frac{1}{0.025}(0.1, 0.09, -0.22) =(4, 3.6,-8.8)\\\\ \\vec{a}^2= \\frac{1}{J} \\vec{a}\_3\\times \\vec{a}\_1=\\frac{1}{0.025}(0.00,-0.05,0.15) =(0, -2,6)\\\\ \\vec{a}^3= \\frac{1}{J} \\vec{a}\_1\\times \\vec{a}\_2=\\frac{1}{0.025}(0.05,0.02,-0.16) =(2, 0.8,-6.4) }\[/latex\]

### Answer 1.c

Calculate \[latex\]\\vec{a}^i \\cdot \\vec{a}\_j\\ (i,j=1,2,3)\[/latex\], we have 9 terms.

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} \\vec{a}^1 \\cdot \\vec{a\_1}=0.80+1.08-0.88=1\\\\ \\vec{a}^1 \\cdot \\vec{a\_2}=0.00-0.60+0.60=0\\\\ \\vec{a}^1 \\cdot \\vec{a\_3}=0.40+0.24-0.64=0\\\\ \\vec{a}^2 \\cdot \\vec{a\_1}=1.60-0.72-0.88=0\\\\ \\vec{a}^2 \\cdot \\vec{a\_2}=0.00+0.40+0.60=1\\\\ \\vec{a}^2 \\cdot \\vec{a\_3}=0.80-0.16-0.64=0\\\\ \\vec{a}^3 \\cdot \\vec{a\_1}=0.40-2.16+1.76=0\\\\ \\vec{a}^3 \\cdot \\vec{a\_2}=0.00+0.12-0.12=0\\\\ \\vec{a}^3 \\cdot \\vec{a\_3}=0.20-0.48+1.28=1\\\\ \\end{aligned} \\right. }\[/latex\]

Directly observe from above terms, we can show that \[latex\]\\vec{a}^i \\cdot \\vec{a}\_j=\\delta^i\_j\[/latex\].

### Answer 1.d

Take cyclic order of (1,2,3).

\[latex\]\\eqalign{ J^\*= \\vec{a}^1 \\cdot (\\vec{a}^2 \\times \\vec{a}^3) = \\begin{vmatrix}4 & 3.6 & -8.8\\\\ 0 & -2 & 6\\\\ 2 & 0.8 & -6.4 \\end{vmatrix} }\[/latex\]

After the calculations, the solution is obtained.

\[latex\]\\eqalign{ J^\*= 51.2+43.2-35.2-19.2= 40 }\[/latex\].

### Answer 1.e

The contravariant components can be obtained by

\[latex\]\\eqalign{ v^i=\\vec{v} \\cdot \\vec{a}^i }\[/latex\].

Therefore, the contravariant components are

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} v^1 = \\vec{v} \\cdot \\vec{a}^1=-20\\\\ v^2 = \\vec{v} \\cdot \\vec{a}^2= \\quad 15\\\\ v^3 = \\vec{v} \\cdot \\vec{a}^3=-10\\\\ \\end{aligned} \\right. }\[/latex\].

The covariant components can be obtained by

\[latex\]\\eqalign{ v\_i=\\vec{v} \\cdot \\vec{a}\_i }\[/latex\].

Therefore, the covariant components are

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} v\_1 = \\vec{v} \\cdot \\vec{a}\_1=-0.55\\\\ v\_2 = \\vec{v} \\cdot \\vec{a}\_2= 1.15\\\\ v\_3 = \\vec{v} \\cdot \\vec{a}\_3= 1.60\\\\ \\end{aligned} \\right. }\[/latex\]

* * *

Question 2
----------

1.  Give a second-rank tensor (dyadic) \[latex\]\\overline{\\overline T} =\\vec{u}\\vec{v}\[/latex\], where \[latex\]\\vec{u}=(3.2,1.4,1.8)\[/latex\] and \[latex\]\\vec{v}=(1,-3,1.5)\[/latex\].
    *   (a) Compute the convariant components (\[latex\]T^{ij}\[/latex\]) of \[latex\]\\overline{\\overline T}\[/latex\] using the base vectors \[latex\] \\vec{a}\_i \[/latex\] given in Problem 1.
    *   (b) Compute the convariant components (\[latex\]T\_{ij}\[/latex\]) of \[latex\]\\overline{\\overline T}\[/latex\] using the reciprocal base vectors \[latex\] \\vec{a}^i \[/latex\] given in Problem 1.
    *   (c) Verify the following expresstion by direct substitution of \[latex\]T^{ij}, \\ \\vec{a}\_i, \\ \\vec{a}^i\[/latex\].
        
        \[latex\]\\eqalign{ T^{ij}\\vec{a\_i}\\vec{a\_j}=\\vec{u}\\vec{v}= \\begin{bmatrix}3.2 & -9.6 & 4.8 \\\\ 1.4 & -4.2 & 2.1 \\\\ 1.8 & -5.4 & 2.7 \\end{bmatrix} }\[/latex\]
        

### Answer 2.a

Substituting \[latex\]\\vec{u},\\vec{v}\[/latex\] for \[latex\]\\vec{a}\_i\[/latex\], we have

\[latex\]\\eqalign{ \\vec{u} = a^1\_u\\vec{a}\_1+a^2\_u\\vec{a}\_2+a^3\_u\\vec{a}\_3 \\\\ \\vec{v} = a^1\_v\\vec{a}\_1+a^2\_v\\vec{a}\_2+a^3\_v\\vec{a}\_3 }\[/latex\]

Now, compute the contravariant components for every term.

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} a^1\_u = \\vec{u}\\cdot \\vec{a}^1 =12.8+5.04-15.84= 2\\\\ a^2\_u = \\vec{u}\\cdot \\vec{a}^2 = 0.00-2.80+10.8=8\\\\ a^3\_u = \\vec{u}\\cdot \\vec{a}^3 = 6.4+1.12-11.52=-4\\\\ \\end{aligned} \\right. }\[/latex\]

and

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} a^1\_v = \\vec{v}\\cdot \\vec{a}^1 =4.0-10.8-13.2= -20\\\\ a^2\_v = \\vec{v}\\cdot \\vec{a}^2 = 0.00+6.00+9.00=15\\\\ a^3\_v = \\vec{v}\\cdot \\vec{a}^3 = 2.00-2.40-9.60=-10\\\\ \\end{aligned} \\right. }\[/latex\]

Thus, multiply \[latex\]\\vec{u}\[/latex\] and \[latex\]\\vec{v}\[/latex\] in terms of \[latex\]\\vec{a}\_i\[/latex\] give us.

\[latex\]\\eqalign{ \\vec{u} \\ \\vec{v}= (2\\vec{a}\_1+8\\vec{a}\_2-4\\vec{a}\_3)(-20\\vec{a}\_1+3\\vec{a}\_2-10\\vec{a}\_3)\\\\ = -40\\vec{a}\_1\\vec{a}\_1+30 \\vec{a}\_1\\vec{a}\_2-20 \\vec{a}\_1\\vec{a}\_3 \\\\ \\quad\\quad -160\\vec{a}\_2\\vec{a}\_1+120 \\vec{a}\_2\\vec{a}\_2-80 \\vec{a}\_2\\vec{a}\_3\\\\ \\quad\\quad +80\\vec{a}\_3\\vec{a}\_1-60 \\vec{a}\_3\\vec{a}\_2+40 \\vec{a}\_3\\vec{a}\_3\\\\ }\[/latex\]

Finally, we obtain \[latex\]T^{ij}\[/latex\]in corresponding terms.

### Answer 2.b

Again, substituting \[latex\]\\vec{u},\\vec{v}\[/latex\] for \[latex\]\\vec{a}^i\[/latex\], we have

\[latex\]\\eqalign{ \\vec{u} = a\_{1u}\\vec{a}^1+a\_{2u}\\vec{a}^2+a\_{3u}\\vec{a}^3 \\\\ \\vec{v} = a\_{1v}\\vec{a}^1+a\_{2v}\\vec{a}^2+a\_{3v}\\vec{a}^3 }\[/latex\]

Now, compute the contravariant components for every term.

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} a\_{1u} = \\vec{u}\\cdot \\vec{a}\_1 =0.64+0.42+0.18= 1.24\\\\ a\_{2u} = \\vec{u}\\cdot \\vec{a}\_2 = 1.28-0.28+0.18=1.18\\\\ a\_{3u} = \\vec{u}\\cdot \\vec{a}\_3 = 0.32-0.84-0.36=-0.88\\\\ \\end{aligned} \\right. }\[/latex\]

and

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} a\_{1v} = \\vec{v}\\cdot \\vec{a}\_1 =0.20-0.90+0.15= -0.55\\\\ a\_{2v} = \\vec{v}\\cdot \\vec{a}\_2 = 0.40+0.60+0.15=1.15\\\\ a\_{3v} = \\vec{v}\\cdot \\vec{a}\_3 = 0.10+1.80-0.30=1.60\\\\ \\end{aligned} \\right. }\[/latex\]

Thus, multiply \[latex\]\\vec{u}\[/latex\] and \[latex\]\\vec{v}\[/latex\] in terms of \[latex\]\\vec{a}^i\[/latex\] give us.

\[latex\]\\eqalign{ \\vec{u} \\ \\vec{v}= (1.24\\vec{a}^1+1.18\\vec{a}^2-0.88\\vec{a}^3)(-0.55 \\vec{a}^1+1.15\\vec{a}^2+1.60\\vec{a}^3)\\\\ = -0.682\\vec{a}^1\\vec{a}^1+1.426 \\vec{a}^1\\vec{a}^2+1.984 \\vec{a}^1\\vec{a}^3 \\\\ \\quad\\quad -0.649\\vec{a}^2\\vec{a}^1+1.357 \\vec{a}^2\\vec{a}^2+1.888 \\vec{a}^2\\vec{a}\_3\\\\ \\quad\\quad +0.484\\vec{a}^3\\vec{a}^1-1.012 \\vec{a}^3\\vec{a}^2-1.408 \\vec{a}^3\\vec{a}^3\\\\ }\[/latex\]

Finally, we obtain \[latex\]T\_{ij}\[/latex\] in corresponding terms.

### Answer 2.c

Consider the following equation

\[latex\]\\eqalign{ \\overline{\\overline T} = T^{ij}\\vec{a\_i}\\vec{a\_j}=\\quad \\quad \\quad\\\\ T^{11}\\vec{a}\_1\\vec{a}\_1+T^{12}\\vec{a}\_1\\vec{a}\_2+T^{13}\\vec{a}\_1\\vec{a}\_3\\\\+ T^{21}\\vec{a}\_2\\vec{a}\_1+T^{22}\\vec{a}\_2\\vec{a}\_2+T^{23}\\vec{a}\_2\\vec{a}\_3\\\\+ T^{31}\\vec{a}\_3\\vec{a}\_1+T^{32}\\vec{a}\_3\\vec{a}\_2+T^{33}\\vec{a}\_3\\vec{a}\_3\\\\ }\[/latex\].

Substituting \[latex\]T^{ij}\[/latex\] we obtain in **Question 2.b** and compute \[latex\]\\vec{a}\_i\\vec{a}\_j\[/latex\], we have,

\[latex\]\\eqalign{ T^{ij}\\vec{a\_i}\\vec{a\_j}=\\qquad \\qquad \\qquad\\qquad \\qquad \\qquad\\qquad \\qquad \\qquad\\\\ -40\\begin{bmatrix}0.04 & 0.06 & 0.02\\\\0.06 & 0.09 & 0.02\\\\0.02 & 0.03 & 0.01 \\end{bmatrix} +\\quad 30\\begin{bmatrix}0.08 & -0.04 & 0.03\\\\0.12 & -0.06 & 0.03\\\\0.04 & -0.02 & 0.01 \\end{bmatrix} -\\quad 20\\begin{bmatrix}0.02 & -0.12 & -0.04\\\\0.03 & -0.18 & -0.02\\\\0.01 & -0.06 & -0.02 \\end{bmatrix} \\\\ -160\\begin{bmatrix}0.08 & 0.012 & 0.04\\\\-0.04 & -0.06 & -0.02\\\\0.02 & 0.03 & 0.01 \\end{bmatrix} +120\\begin{bmatrix}0.16 & -0.08 & 0.04\\\\-0.08 & 0.04 & -0.02\\\\0.04 & -0.02 & 0.01 \\end{bmatrix} -80\\begin{bmatrix}0.04 & -0.24 & -0.08\\\\-0.02 & 0.12 & 0.04\\\\0.01 & -0.06 & -0.02 \\end{bmatrix} \\\\ +80\\begin{bmatrix}0.02 & 0.03 & 0.01\\\\-0.12 & -0.18 & -0.06\\\\-0.04 & -0.06 & -0.02 \\end{bmatrix} -60\\begin{bmatrix}0.04 & -0.02 & 0.01\\\\-0.24 & 0.12 & -0.06\\\\-0.08 & 0.04 & -0.02 \\end{bmatrix} +40\\begin{bmatrix}0.01 & -0.06 & -0.02\\\\-0.06 & 0.36 & 0.12\\\\-0.02 & 0.12 & 0.04 \\end{bmatrix} }\[/latex\].

. Rearrange this equation, we shows that

\[latex\]\\eqalign{ T^{ij}\\vec{a\_i}\\vec{a\_j}=\\vec{u}\\ \\vec{v}= \\begin{bmatrix}3.2 & -9.6 & 4.8\\\\1.4 & -4.2 & 2.1\\\\1.8 & -5.4 & 2.7 \\end{bmatrix} }\[/latex\].

.