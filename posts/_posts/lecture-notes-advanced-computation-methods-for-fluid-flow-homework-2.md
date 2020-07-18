---
title: '[Lecture Notes] Advanced Computation Methods for Fluid Flow – Homework 2'
tags:
  - Advanced Computation Methods for Fluid Flow - 2018
  - computational fluid dynamics
  - numerical method
id: '623'
date: 2018-04-17 15:51:29
---

> _14/04/2018, Homework No. 2_

* * *

Description
-----------

Given the Cartesian coordinates \[latex\](x\_i,y\_i,z\_i)\[/latex\] for 8 corner nodes of the following numerical element: \[latex\]\\textbf{P1}:(-1,1,1)\[/latex\], \[latex\]\\textbf{P2}:(0, 0, 3)\[/latex\], \[latex\]\\textbf{P3}:(2.5, 1, 6)\[/latex\], \[latex\]\\textbf{P4}:(1, 2, 4)\[/latex\], \[latex\]\\textbf{P5}:(1, 3, 7)\[/latex\], \[latex\]\\textbf{P6}:(2.5, 1.5, 9)\[/latex\], \[latex\]\\textbf{P7}:(4.5, 2, 12.5)\[/latex\], \[latex\]\\textbf{P8}:(3, 4, 10)\[/latex\].

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/未命名-13.png)

### Question 1.a

Construct the covariant base vectors \[latex\]\\vec{a}\_i \\ (i=1,2,3)\[/latex\] along the \[latex\]\\xi^i\[/latex\]-direction using nodes \[latex\] (\\textbf{P1},\\textbf{P2},\\textbf{P4},\\textbf{P5})\[/latex\].  

*   **Answer** \[latex\]\\vec{a}\_i\[/latex\] is the change of \[latex\]\\vec{r}\[/latex\] in \[latex\]\\xi^i\[/latex\] direction. And it can be expressed as
    
    \[latex\]\\eqalign{ \\vec{a}\_i = \\frac{\\partial \\vec{r}}{\\partial \\xi^i}. }\[/latex\]
    
    Thus, the covariant base vectors are obtained by
    
    \[latex\]\\eqalign{ \\vec{a}\_1 = \\frac{\\textbf{P2}-\\textbf{P1}}{\\Delta \\xi^1} = \\frac{(0, 0, 3)-(-1,1,1)}{1} = (1,-1,2),\\\\ \\vec{a}\_2 = \\frac{\\textbf{P4}-\\textbf{P1}}{\\Delta \\xi^2} = \\frac{(1, 2, 4)-(-1,1,1)}{1} =\\quad (2,1,3),\\\\ \\vec{a}\_3 = \\frac{\\textbf{P5}-\\textbf{P1}}{\\Delta \\xi^3} = \\frac{(1, 3, 7)-(-1,1,1)}{1} =\\quad (2,2,6). }\[/latex\]
    

* * *

### Question 1.b

Determine the volume of the numerical element.  

*   **Answer** \[latex\]\\eqalign{ d\\vec{r} = \\textbf{P7}-\\textbf{P1} = (5.5,1,11.5)= d\\xi^1 \\vec{a}\_1 + d\\xi^2 \\vec{a}\_2 + d\\xi^3 \\vec{a}\_3 \\\\= d\\xi^1 (1,-1,2) + d\\xi^2 (2,1,3) + d\\xi^3 (2,2,6) }\[/latex\]. Rewrite this equation in matrix form, we have
    
    \[latex\]\\eqalign{ \\begin{bmatrix}1 & 2 &2\\\\-1 & 1 &2\\\\2 & 3 &6 \\end{bmatrix}\\begin{bmatrix}d\\xi^1 \\\\d\\xi^2\\\\d\\xi^3 \\end{bmatrix} = \\begin{bmatrix}5.5 \\\\1\\\\11.5 \\end{bmatrix} }\[/latex\]
    
    By solving the linear system above, we obtain \[latex\]d\\xi^1, \\ d\\xi^2,\\ d\\xi^3 \[/latex\] are \[latex\]\\frac{67}{26}, \\ \\frac{21}{26}, \\ \\frac{17}{26}\[/latex\], respectively. Jocobian \[latex\]J\[/latex\] of \[latex\]\\vec{a}\_i\[/latex\] is
    
    \[latex\]\\eqalign{ J= \\vec{a}\_1 \\cdot (\\vec{a}\_2 \\times \\vec{a}\_3) = \\begin{vmatrix}1 & -1 & 2\\\\ 2 & 1 & 3\\\\ 2 & 2 & 6 \\end{vmatrix} =10 }\[/latex\]
    
    Differential volume enclosed by \[latex\]d\\xi^1 \\vec{a}\_1, d\\xi^2 \\vec{a}\_2, d\\xi^3 \\vec{a}\_3 \[/latex\] is computed by \[latex\]J\\ d\\xi^1 d\\xi^2 d\\xi^3 = 13.60889\[/latex\].

* * *

### Question 1.c

Calculate the metric tensor \[latex\]g\_{ij}\[/latex\] and determine the angles \[latex\]\\theta\_{ij}\[/latex\] between \[latex\]\\xi^i\[/latex\] and \[latex\]\\xi^j\[/latex\] axes \[latex\]( i, j = 1, 2, 3)\[/latex\].  

*   **Answer** Compute \[latex\] g\_{ij} \[/latex\].
    
    \[latex\]\\eqalign{ \\left\\{ \\begin{aligned} & g\_{11}=\\vec{a}\_1 \\cdot \\vec{a}\_1 = 1+1+4=6,\\\\ & g\_{22}=\\vec{a}\_2 \\cdot \\vec{a}\_2 = 4+ 1+9=14\\\\ & g\_{33}=\\vec{a}\_3 \\cdot \\vec{a}\_3 = 4+4+36=44\\\\ & g\_{12}=\\vec{a}\_1 \\cdot \\vec{a}\_2 = 2-1+6=7=g\_{21}\\\\ & g\_{13}=\\vec{a}\_1 \\cdot \\vec{a}\_3 = 2-2+12=12=g\_{31}\\\\ & g\_{23}=\\vec{a}\_2 \\cdot \\vec{a}\_3 = 4+2+18=24=g\_{32}\\\\ \\end{aligned} \\right. }\[/latex\]
    
    From the definition of inner product, we have
    
    \[latex\]\\eqalign{ cos \\theta\_{ij} = \\frac{\\vec{a}\_i \\cdot \\vec{a}\_j}{|\\vec{a}\_i||\\vec{a}\_j|} = \\frac{\\sqrt{g\_{ij}}}{g\_{ii}g\_{jj}} }\[/latex\].
    
    Then, every \[latex\]\\theta\_{ij}\[/latex\] can be obtain
    
    \[latex\]\\eqalign{ \\left\\{ \\begin{aligned} & \\theta\_{11}=\\arccos(\\frac{g\_{11}}{\\sqrt{g\_{11}g\_{11}}})=1,\\\\ & \\theta\_{22}=\\arccos(\\frac{g\_{22}}{\\sqrt{g\_{22}g\_{22}}})=1,\\\\ & \\theta\_{33}=\\arccos(\\frac{g\_{11}}{\\sqrt{g\_{33}g\_{33}}})=1,\\\\ & \\theta\_{12}=\\arccos(\\frac{g\_{12}}{\\sqrt{g\_{11}g\_{22}}})=0.7016=\\theta\_{21},\\\\ & \\theta\_{13}=\\arccos(\\frac{g\_{13}}{\\sqrt{g\_{11}g\_{33}}})=0.7398=\\theta\_{31},\\\\ & \\theta\_{23}=\\arccos(\\frac{g\_{23}}{\\sqrt{g\_{22}g\_{33}}})=0.2576=\\theta\_{32},\\\\ \\end{aligned} \\right. }\[/latex\]
    

* * *

### Question 1.d

Calculate the conjugate metric tensor \[latex\]g^{ij}\[/latex\] from \[latex\]g\_{ij}\[/latex\] without actually forming the reciprocal basis \[latex\]\\vec{a}^i\[/latex\].  

*   **Answer** With the cyclic (imn), (jpq) there exits a relationship beteween covariant and contravariant metric tensor.
    
    \[latex\]\\eqalign{ g^{ij} = \\frac{1}{\\textbf{g}}(g\_{mp}g\_{nq}-g\_{mq}g\_{np}) }\[/latex\]
    
    where \[latex\]\\textbf{g} \[/latex\] equal to \[latex\]J^2=100\[/latex\]. Every \[latex\]g^{ij}\[/latex\] can be obtain as follow
    
    \[latex\]\\eqalign{ \\left\\{ \\begin{aligned} & g^{11} = \\frac{1}{\\textbf{g}}(g\_{22}g\_{33}-g\_{23}g\_{32})=\\frac{40}{100}=0.4\\\\ & g^{22} = \\frac{1}{\\textbf{g}}(g\_{33}g\_{11}-g\_{13}g\_{31})=\\frac{120}{100}=1.20\\\\ & g^{33} = \\frac{1}{\\textbf{g}}(g\_{11}g\_{22}-g\_{12}g\_{21})=\\frac{35}{100}=0.35\\\\ & g^{12} = \\frac{1}{\\textbf{g}}(g\_{13}g\_{23}-g\_{12}g\_{33})=\\frac{-20}{100}=-0.20=g^{21}\\\\ & g^{13} = \\frac{1}{\\textbf{g}}(g\_{12}g\_{23}-g\_{13}g\_{22})=\\frac{0}{100}=0.0=g^{31}\\\\ & g^{23} = \\frac{1}{\\textbf{g}}(g\_{12}g\_{13}-g\_{23}g\_{11})=\\frac{-60}{100}=-0.6=g^{32}\\\\ \\end{aligned} \\right. }\[/latex\]
    

* * *

### Question 1.e

Verify the expression of identity matrix \[latex\]\\overline{\\overline{I}}=g^{ij}\\vec{a}\_i\\vec{a}\_j\[/latex\] by direct substitution of \[latex\]g^{ij}\[/latex\] and base vectors \[latex\]\\vec{a}\_i\[/latex\].  

*   **Answer** Expand the equation, we have
    
    \[latex\]\\eqalign{ \\begin{align} g^{ij}\\vec{a}\_i\\vec{a}\_j & = g^{11}\\vec{a}\_1\\vec{a}\_1+g^{12}\\vec{a}\_1\\vec{a}\_2+g^{13}\\vec{a}\_1\\vec{a}\_3\\\\ & + g^{21}\\vec{a}\_2\\vec{a}\_1+ g^{22}\\vec{a}\_2\\vec{a}\_2+ g^{23}\\vec{a}\_2\\vec{a}\_3\\\\ & + g^{31}\\vec{a}\_3\\vec{a}\_1+ g^{32}\\vec{a}\_3\\vec{a}\_2+ g^{33}\\vec{a}\_3\\vec{a}\_3\\\\ \\end{align} }\[/latex\]
    
    Substituting covariant base vectors we obtain in Question 1.a and contravariant metric tensor into above equation.
    
    \[latex\]\\begin{align} g^{ij}\\vec{a}\_i\\vec{a}\_j & = 0.4\\begin{bmatrix}1 & -1 & 2 \\\\-1 & 1 & -2\\\\2 & -2 & 4 \\end{bmatrix}+ 0.36\\begin{bmatrix}2 & -2 & 4 \\\\1 & -1 & 2\\\\3 & -3 & 6 \\end{bmatrix}+ 0.0\\begin{bmatrix}2 & -2 & 4 \\\\2 & -2 & 4\\\\6 & -6 & 12 \\end{bmatrix}\\\\ & + 0.36\\begin{bmatrix}2 & 1 & 3 \\\\-2 & -1 & -3\\\\4 & 2 & 6 \\end{bmatrix}+ 1.20\\begin{bmatrix}4 & 2 & 6 \\\\2 & 1 & 3\\\\6 & 3 & 9 \\end{bmatrix}- 0.60\\begin{bmatrix}4 & 2 & 6 \\\\4 & 2 & 6\\\\12 & 6 & 18 \\end{bmatrix}\\\\ & + 0.00\\begin{bmatrix}2 & 2 & 6 \\\\-2 & -2 & -6\\\\4 & 4 & 12 \\end{bmatrix}- 0.60\\begin{bmatrix}4 & 4 & 12 \\\\2 & 2 & 6\\\\6 & 6 & 18 \\end{bmatrix}- 0.35\\begin{bmatrix}4 & 4 & 12 \\\\4 & 4 & 12\\\\12 & 12 & 36 \\end{bmatrix}\\\\ & = \\begin{bmatrix}1 & 0 & 0 \\\\0 & 1 & 0\\\\0 & 0 & 1 \\end{bmatrix}= \\overline{\\overline{I}} \\end{align} \[/latex\]
    

* * *

### Question 1.f

Given two vectors \[latex\]\\vec{u}\[/latex\] and \[latex\]\\vec{v}\[/latex\] with contravariant components \[latex\]u^i=(3,2,-1)\[/latex\], \[latex\]v^i=(5,-4,2)\[/latex\] find the associated covariant vector components \[latex\]u\_i\[/latex\] and \[latex\]v\_i\[/latex\].  

*   **Answer** The contravariant components can be transfer into covariant components by following equation \[latex\]A\_i = g\_{ij}A^j\[/latex\]. Thus, the covariant components \[latex\]u\_i\[/latex\] and \[latex\]v\_i\[/latex\] can be obtained by

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} & u\_{1}=g\_{11}u^1+g\_{12}u^2+g\_{13}u^3=6\\times3 +7\\times2+12\\times(-1)=20\\\\ & u\_{2}=g\_{21}u^1+g\_{22}u^2+g\_{23}u^3=7\\times3 +14\\times2+24\\times(-1)=25\\\\ & u\_{3}=g\_{31}u^1+g\_{32}u^2+g\_{33}u^3=12\\times3 +24\\times2+44\\times(-1)=40\\\\ \\end{aligned} \\right. }\[/latex\]

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} & v\_{1}=g\_{11}v^1+g\_{12}v^2+g\_{13}v^3=6\\times5 +7\\times(-4)+12\\times2=26\\\\ & v\_{2}=g\_{21}v^1+g\_{22}v^2+g\_{23}v^3=7\\times5 +14\\times(-4)+24\\times2=27\\\\ & v\_{3}=g\_{31}v^1+g\_{32}v^2+g\_{33}v^3=12\\times5 +24\\times(-4)+44\\times2=52\\\\ \\end{aligned} \\right. }\[/latex\]

* * *

### Question 1.g

Determine the Cartesian components of vectors \[latex\]\\vec{u}\[/latex\] and \[latex\]\\vec{v}\[/latex\].  

*   **Answer**
    
    \[latex\]\\eqalign{ \\vec{u} =u^i\\vec{a}\_i=3(1,-1,2)+2(2,1,3)-(2,2,6)=(5,-3,6)\\\\ \\vec{v} =v^i\\vec{a}\_i=5(1,-1,2)-4(2,1,3)+2(2,2,6)=(1,-5,10) }\[/latex\]
    

* * *

### Question 1.h

Evaluate the inner (dot) product \[latex\]\\vec{u}\\cdot \\vec{v}\[/latex\] in \[latex\]\\left\\{\\vec{a}\_i,\\vec{a}\_j\\right\\}\[/latex\], \[latex\]\\left\\{\\vec{a}^i,\\vec{a}^j\\right\\}\[/latex\], \[latex\]\\left\\{\\vec{a}^i,\\vec{a}\_j\\right\\}\[/latex\], and \[latex\]\\left\\{\\vec{a}\_i,\\vec{a}^j\\right\\}\[/latex\] bases.  

*   **Answer**
    
    \[latex\]\\eqalign{ \\begin{aligned} \\vec{u}\\cdot\\vec{v} & = (u^i\\vec{a}\_i)\\cdot(v^j\\vec{a}\_j)= u^iv^j\\ \\vec{a}\_i\\cdot\\vec{a}\_j=g\_{ij} u^iv^j\\\\ &=6\\times3\\times5+7\\times3\\times(-4) +12\\times3\\times2\\\\ &\\quad +7\\times2\\times5+14\\times2\\times(-4) +24\\times2\\times2\\\\ &\\quad+ 12\\times(-1)\\times5+24\\times(-1)\\times(-4) +44\\times(-1)\\times2\\\\ &=80 \\\\ \\\\ \\vec{u}\\cdot\\vec{v} & = (u\_i\\vec{a}^i)\\cdot(v\_j\\vec{a}^j)= u\_iv\_j\\ \\vec{a}^i\\cdot\\vec{a}^j=g^{ij} u\_iv\_j\\\\ &=0.40\\times20\\times26-0.20\\times20\\times27 +0.0\\times20\\times52\\\\ &\\quad -0.20\\times25\\times26+1.20\\times25\\times27 -0.60\\times25\\times52\\\\ &\\quad +0.0\\times40\\times26-0.60\\times40\\times27 +0.35\\times40\\times52\\\\ &=80 \\\\ \\\\ \\vec{u}\\cdot\\vec{v} & = (u^i\\vec{a}\_i)\\cdot(v\_j\\vec{a}^j)= u^iv\_j\\ \\vec{a}\_i\\cdot\\vec{a}^j=\\delta^j\_i u^iv\_j= u^iv\_i\\\\ &=3\\times26+2\\times27+(-1)\\times52\\\\ &=80 \\\\ \\\\ \\vec{u}\\cdot\\vec{v} & = (u\_i\\vec{a}^i)\\cdot(v^j\\vec{a}\_j)= u\_iv^j\\ \\vec{a}^i\\cdot\\vec{a}\_j=\\delta\_j^i u\_iv^j= u\_iv^i\\\\ &=20\\times5+25\\times(-4)+40\\times2\\\\ &=80 \\end{aligned} }\[/latex\]
    

* * *

### Question 1.i

Express the cross product \[latex\]\\vec{u}\\times \\vec{v}\[/latex\] in covariant basis \[latex\]\\vec{a}\_i\[/latex\].  

*   **Answer**
    
    \[latex\]\\eqalign{ \\begin{aligned} \\vec{u}\\times\\vec{v} & = (u\_i\\vec{a}^i)\\times(v\_j\\vec{a}^j)= u\_iv\_j\\ (\\vec{a}^i\\times\\vec{a}^j)\\\\ &=u\_iv\_j(\\vec{a}^i\\times\\vec{a}^j)^k\\ \\vec{a}\_k\\\\ &= u\_iv\_j(\\vec{a}^i\\times\\vec{a}^j)\\cdot\\vec{a}^k\\ \\vec{a}\_k\\\\ &= u^iv^je^{kij}\\ \\vec{a}\_k\\\\ &= u\_iv\_j \\frac{1}{J}\\ \\vec{a}\_k\\\\ &=\\frac{1}{10}u\_iv\_j \\vec{a}\_k\\\\ \\end{aligned} }\[/latex\]
    

* * *

### Question 1.j

Express the cross product \[latex\]\\vec{u}\\times \\vec{v}\[/latex\] in contravariant basis \[latex\]\\vec{a}^i\[/latex\].  

*   **Answer**
    
    \[latex\]\\eqalign{ \\begin{aligned} \\vec{u}\\times\\vec{v} & = (u^i\\vec{a}\_i)\\times(v^j\\vec{a}\_j)= u^iv^j\\ (\\vec{a}\_i\\times\\vec{a}\_j)\\\\ &=u^iv^j(\\vec{a}\_i\\times\\vec{a}\_j)\_k\\ \\vec{a}^k\\\\ &= u^iv^j(\\vec{a}\_i\\times\\vec{a}\_j)\\cdot\\vec{a}\_k\\ \\vec{a}^k\\\\ &= u^iv^je\_{kij}\\ \\vec{a}^k\\\\ &= u^iv^j J\\ \\vec{a}^k\\\\ &=10u^iv^j \\vec{a}^k\\\\ \\end{aligned} }\[/latex\]
    

* * *

### Question 1.k

Given the Cartesian components of a second-rank tensor \[latex\]\\overline{\\overline{T}}\[/latex\].

\[latex\]\\eqalign{ \\overline{\\overline{T}} =\\begin{bmatrix}T\_{xx} & T\_{xy} & T\_{xz}\\\\T\_{yx} & T\_{yy} & T\_{yz}\\\\T\_{zx} & T\_{zy} & T\_{zz} \\end{bmatrix} =\\begin{bmatrix}5 &3 & -2\\\\2 & 6 & -1\\\\3 & -4 & \\ 2 \\end{bmatrix} }\[/latex\].

find the associated covariant tensor components \[latex\]T\_{ij}\[/latex\]  

*   **Answer** \[latex\]T\_{ij}\[/latex\] can be evaluated by following equation
    
    \[latex\]\\eqalign{ \\begin{aligned} T\_{ij} = \\vec{a}\_i\\cdot \\overline{\\overline{T}} \\cdot \\vec{a}\_j \\end{aligned} }\[/latex\].
    
    Each \[latex\]T\_{ij}\[/latex\] are

\[latex\]\\eqalign{ \\begin{aligned} T\_{11} & = \\vec{a}\_1\\cdot\\overline{\\overline{T}}\\cdot \\vec{a}\_1 \\\\ &=\\begin{bmatrix}1 &-1 & 2 \\end{bmatrix} \\begin{bmatrix}5 &3 & -2\\\\2 & 6 & -1\\\\3 & -4 & \\ 2 \\end{bmatrix} \\begin{bmatrix}1 \\\\-1 \\\\ 2 \\end{bmatrix}\\\\ &= 26\\\\ \\\\ T\_{12} & = \\vec{a}\_1\\cdot\\overline{\\overline{T}}\\cdot \\vec{a}\_2 =16\\\\ \\\\ T\_{13} & = \\vec{a}\_1\\cdot\\overline{\\overline{T}}\\cdot \\vec{a}\_3 =14\\\\ \\\\ T\_{21} & = \\vec{a}\_2\\cdot\\overline{\\overline{T}}\\cdot \\vec{a}\_1 =23\\\\ \\\\ T\_{22} & = \\vec{a}\_2\\cdot\\overline{\\overline{T}}\\cdot \\vec{a}\_2 =45\\\\ \\\\ T\_{23} & = \\vec{a}\_2\\cdot\\overline{\\overline{T}}\\cdot \\vec{a}\_3 =48\\\\ \\\\ T\_{31} & = \\vec{a}\_3\\cdot\\overline{\\overline{T}}\\cdot \\vec{a}\_1 =50\\\\ \\\\ T\_{32} & = \\vec{a}\_3\\cdot\\overline{\\overline{T}}\\cdot \\vec{a}\_3 =76\\\\ \\\\ T\_{33} & = \\vec{a}\_3\\cdot\\overline{\\overline{T}}\\cdot \\vec{a}\_3 =88\\\\ \\\\ \\end{aligned} } \[/latex\].

### Question 1.l

Find the associated contravariant tensor components \[latex\]T^{ij}\[/latex\] directly from \[latex\]T\_{ij}\[/latex\] without forming the reciprocal base vectors.  

*   **Answer** Using mtetrix tensors, the contravariant tensor components \[latex\]T^{ij}\[/latex\] can be found from \[latex\]T\_{ij}\[/latex\] directly.
    
    \[latex\]\\eqalign{ T^{ij}=g^{im}g^{jn}T\_{mn} }\[/latex\].
    
    Each \[latex\]T^{ij}\[/latex\] are
    
    \[latex\]\\eqalign{ \\begin{aligned} T^{11}&=g^{1m}g^{1n}T\_{mn}\\\\ &\\quad +g^{11}g^{11}T\_{11}+g^{11}g^{12}T\_{12}+g^{11}g^{13}T\_{13}\\\\ &\\quad +g^{12}g^{11}T\_{21}+g^{12}g^{12}T\_{22}+g^{12}g^{13}T\_{23}\\\\ &\\quad +g^{13}g^{11}T\_{31}+g^{13}g^{13}T\_{32}+g^{13}g^{13}T\_{33}\\\\ &=2.84 \\\\ \\\\ T^{12}&=g^{1m}g^{2n}T\_{mn}=-1.88\\\\ \\\\ T^{13}&=g^{1m}g^{3n}T\_{mn}=0.16\\\\ \\\\ T^{21}&=g^{2m}g^{1n}T\_{mn}=-4.08\\\\ \\\\ T^{22}&=g^{2m}g^{2n}T\_{mn}=6.56\\\\ \\\\ T^{23}&=g^{2m}g^{3n}T\_{mn}=-2.42\\\\ \\\\ T^{31}&=g^{3m}g^{1n}T\_{mn}=1.56\\\\ \\\\ T^{32}&=g^{3m}g^{2n}T\_{mn}=-2.42\\\\ \\\\ T^{33}&=g^{3m}g^{3n}T\_{mn}=0.94\\\\ \\\\ \\end{aligned} } \[/latex\].