---
title: '[Lecture Notes] Advanced Computation Methods for Fluid Flow – Homework 3'
tags:
  - Advanced Computation Methods for Fluid Flow - 2018
  - computational fluid dynamics
  - numerical method
id: '726'
date: 2018-04-27 00:15:37
---

> _23/04/2018, Homework No. 3_

* * *

Question 1.a
------------

Express the following covariant derivatives in terms of partial derivatives and Christoffel symbols:

\[latex\]\\eqalign{ (a) \\quad\\nabla\\cdot\\overline{\\overline{\\sigma}} = \\sigma^{ji}\_{,j}\\vec{a}\_i }\[/latex\]

  

*   **Answer** Using Christoffel symbols:
    
    \[latex\]\\eqalign{ \\begin{align} \\nabla\\cdot\\overline{\\overline{\\sigma}} &=\\vec{a}^m \\cdot \\frac{\\partial \\overline{\\overline{\\sigma}}}{\\partial \\xi^m}= \\vec{a}^m \\cdot \\frac{\\partial (\\sigma^{ij}\\vec{a}\_i\\vec{a}\_j)}{\\partial \\xi^m} \\\\ &=\\vec{a}^m \\cdot\\left\[ \\frac{\\partial \\sigma^{ij}}{\\partial \\xi^m}\\vec{a}\_i\\vec{a}\_j+ \\sigma^{ij}\\left(\\frac{\\partial \\vec{a}\_i}{\\partial \\xi^m}\\vec{a}\_j+ \\vec{a}\_i\\frac{\\partial \\vec{a}\_j}{\\partial \\xi^m} \\right)\\right\] \\\\ &=\\vec{a}^m \\cdot\\left\[ \\frac{\\partial \\sigma^{ij}}{\\partial \\xi^m}\\vec{a}\_i\\vec{a}\_j+ \\sigma^{ij}\\left(\\Gamma^n\_{im}\\vec{a}\_n\\vec{a}\_j+ \\vec{a}\_i\\Gamma^n\_{jm}\\vec{a}\_n \\right)\\right\] \\\\ &=\\vec{a}^m \\cdot\\left\[ \\frac{\\partial \\sigma^{ij}}{\\partial \\xi^m}\\vec{a}\_i\\vec{a}\_j+ \\left(\\sigma^{nj}\\Gamma^i\_{nm}\\vec{a}\_i\\vec{a}\_j+ \\sigma^{in}\\Gamma^j\_{nm}\\vec{a}\_i\\vec{a}\_j \\right)\\right\] \\\\ &=\\vec{a}^m \\cdot\\left\[\\left( \\frac{\\partial \\sigma^{ij}}{\\partial \\xi^m}+\\sigma^{nj}\\Gamma^i\_{nm}+ \\sigma^{in}\\Gamma^j\_{nm} \\right) \\vec{a}\_i\\vec{a}\_j\\right\] \\\\ &=\\vec{a}^m \\cdot\\left( \\sigma^{ij}\_{,m} \\vec{a}\_i\\vec{a}\_j \\right) = (\\vec{a}^m\\cdot\\vec{a}\_i )\\sigma^{ij}\_{,m} \\vec{a}\_j\\\\ &=\\delta^m\_i\\sigma^{ij}\_{,m} \\vec{a}\_j = \\sigma^{ij}\_{,i} \\vec{a}\_j =\\sigma^{ji}\_{,j} \\vec{a}\_i \\end{align} }\[/latex\]
    

* * *

Question 1.b
------------

Express the following covariant derivatives in terms of partial derivatives and Christoffel symbols:

\[latex\]\\eqalign{ (b) \\quad\\nabla^2\\vec{v} = g^{jk}\\ v^i\_{,jk}\\ \\vec{a}\_i }\[/latex\]

  

*   **Answer**

\[latex\]\\eqalign{ \\quad\\nabla^2\\vec{v} &= \\nabla\\cdot\\left\[\\nabla (v^i\\vec{a}\_i)\\right\] = \\nabla\\cdot\\left(\\vec{a}^jv^i\_{,j}\\vec{a}\_i\\right) =\\vec{a}^k\\cdot\\left(\\vec{a}^jv^i\_{,j}\\vec{a}\_i\\right)\_{,k} \\\\ &=\\left(\\vec{a}^k\\cdot\\vec{a}^j\\right) \\left(v^i\_{,j}\\vec{a}\_i\\right)\_{,k}=g^{jk}v^i\_{,jk}\\vec{a}\_i\\\\ &=g^{jk} \\left(\\frac{\\partial D^i\_j}{\\partial \\xi^k}+\\Gamma^i\_{nk} D^n\_j-\\Gamma^n\_{jk} D^i\_n\\right)\\vec{a}\_i\\\\ &=g^{jk} \\left\[\\frac{\\partial}{\\partial \\xi^k}\\left(\\frac{\\partial v^i}{\\partial \\xi^j}+\\Gamma^i\_{nm}v^n\\right)+\\Gamma^i\_{nk} \\left(\\frac{\\partial v^n}{\\partial \\xi^j}+\\Gamma^n\_{pm}v^p\\right)-\\Gamma^n\_{jk} \\left(\\frac{\\partial v^i}{\\partial \\xi^n}+\\Gamma^i\_{pn}v^p\\right)\\right\]\\vec{a}\_i\\\\ &=g^{jk} \\left\[\\frac{\\partial}{\\partial \\xi^k}\\left(\\frac{\\partial v^i}{\\partial \\xi^j}+\\Gamma^i\_{pm}v^p\\right)+\\Gamma^i\_{nk} \\left(\\frac{\\partial v^n}{\\partial \\xi^j}+\\Gamma^n\_{pm}v^p\\right)-\\Gamma^n\_{jk} \\left(\\frac{\\partial v^i}{\\partial \\xi^n}+\\Gamma^i\_{pn}v^p\\right)\\right\]\\vec{a}\_i }\[/latex\]

* * *

Question 2.a
------------

Given the spherical coordinate system \[latex\]( r,\\ \\theta ,\\ \\phi )\[/latex\] with

\[latex\]\\eqalign{ x=r \\cos\\theta, \\quad y=r\\ sin\\theta cos\\phi, \\quad z=r \\ sin\\theta sin\\phi }\[/latex\]

Calculate metric tensor \[latex\]g\_{ij}\[/latex\] and conjugate metric tensor \[latex\]g^{ij}\[/latex\].  

*   **Answer** Find the covariant base vectors for this spherical coordinate system.
    
    \[latex\]\\eqalign{ \\vec{a}\_i=\\frac{\\partial \\vec{r} }{\\partial \\xi^i }= ( \\frac{\\partial (rcos\\theta) }{\\partial \\xi^i },\\ \\frac{\\partial (rsin\\theta cos\\phi) }{\\partial \\xi^i },\\ \\frac{\\partial rsin\\theta sin\\phi) }{\\partial \\xi^i }\\ ) }\[/latex\]
    
    Each covariant base vector can be written as
    
    \[latex\]\\eqalign{ \\left\\{ \\begin{aligned} &\\vec{a}\_1= ( \\frac{\\partial (rcos\\theta) }{\\partial r },\\ \\frac{\\partial (rsin\\theta cos\\phi) }{\\partial r },\\ \\frac{\\partial (rsin\\theta sin\\phi) }{\\partial r }\\ ) =(cos\\theta, \\ sin\\theta cos\\phi, \\ sin\\theta sin\\phi \\ ) \\\\ &\\vec{a}\_2= ( \\frac{\\partial (rcos\\theta) }{\\partial \\theta },\\ \\frac{\\partial (rsin\\theta cos\\phi) }{\\partial \\theta },\\ \\frac{\\partial (rsin\\theta sin\\phi) }{\\partial \\theta }\\ ) =( -rsin\\theta, \\ rcos\\theta cos\\phi, \\ rcos\\theta sin\\phi\\ )\\\\ &\\vec{a}\_3= ( \\frac{\\partial (rcos\\theta) }{\\partial \\phi },\\ \\frac{\\partial (rsin\\theta cos\\phi) }{\\partial \\phi },\\ \\frac{\\partial (rsin\\theta sin\\phi) }{\\partial \\phi }\\ ) =( 0, \\ -rsin\\theta sin\\phi, \\ rsin\\theta cos\\phi\\ ) \\end{aligned} \\right. }\[/latex\]
    
    Then, we can calculate every component of metric tensor \[latex\]g\_{ij}\[/latex\].
    
    \[latex\]\\eqalign{ \\left\\{ \\begin{aligned} & g\_{11}=\\vec{a}\_1 \\cdot \\vec{a}\_1 = cos^2\\theta+sin^2\\theta cos^2\\phi+sin^2\\theta sin^2\\phi=1,\\\\ & g\_{22}=\\vec{a}\_2 \\cdot \\vec{a}\_2 = r^2sin^2\\theta+r^2cos^2\\theta cos^2\\phi+r^2cos^2\\theta sin^2\\phi=r^2,\\\\ & g\_{33}=\\vec{a}\_3 \\cdot \\vec{a}\_3 = 0+r^2sin^2\\theta sin^2\\phi+r^2sin^2\\theta cos^2\\phi=r^2sin^2\\theta,\\\\ & g\_{12}=\\vec{a}\_1 \\cdot \\vec{a}\_2 = -rsin\\theta cos\\theta+rcos\\theta sin\\theta cos^2\\phi+rsin\\theta cos\\theta sin^2\\phi=0 = g\_{21},\\\\ & g\_{13}=\\vec{a}\_1 \\cdot \\vec{a}\_3 = 0-rsin^2\\theta sin\\phi cos\\phi+rsin^2\\theta sin\\phi cos\\phi=0 =g\_{31}\\\\ & g\_{23}=\\vec{a}\_2 \\cdot \\vec{a}\_3 = 0-r^2sin\\theta cos\\theta sin\\phi cos\\phi+rsin\\theta cos\\theta sin\\phi cos\\phi=0 =g\_{32}\\\\ \\end{aligned} \\right. }\[/latex\]
    
    With the cyclic (imn), (jpq) there exits a relationship beteween covariant and contravariant metric tensor.
    
    \[latex\]\\eqalign{ g^{ij} = \\frac{1}{\\textbf{g}}(g\_{mp}g\_{nq}-g\_{mq}g\_{np}) }\[/latex\]
    
    where \[latex\]\\textbf{g}\[/latex\] equal to \[latex\]J^2=r^4sin^2\\theta\[/latex\]. Every component of conjuga \[latex\]g^{ij}\[/latex\] can be obtain as follow
    
    \[latex\]\\eqalign{ \\left\\{ \\begin{aligned} & g^{11} = \\frac{1}{\\textbf{g}}(g\_{22}g\_{33}-g\_{23}g\_{32})=\\frac{r^4sin^2\\theta}{r^4sin^2\\theta}=1\\\\ & g^{22} = \\frac{1}{\\textbf{g}}(g\_{33}g\_{11}-g\_{13}g\_{31})=\\frac{r^2sin^2\\theta}{r^4sin^2\\theta}=\\frac{1}{r^2}\\\\ & g^{33} = \\frac{1}{\\textbf{g}}(g\_{11}g\_{22}-g\_{12}g\_{21}=\\frac{r^2}{r^4sin^2\\theta}=\\frac{1}{r^2sin^2\\theta}\\\\ & g^{12} = \\frac{1}{\\textbf{g}}(g\_{13}g\_{23}-g\_{12}g\_{33})=0=g^{21}\\\\ & g^{13} = \\frac{1}{\\textbf{g}}(g\_{12}g\_{23}-g\_{13}g\_{22})=0=g^{31}\\\\ & g^{23} = \\frac{1}{\\textbf{g}}(g\_{12}g\_{13}-g\_{23}g\_{11})=0=g^{32}\\\\ \\end{aligned} \\right. }\[/latex\]
    

* * *

Question 2.b
------------

Compute Christoffel symbols \[latex\]\\Gamma^i\_{jk}\[/latex\] in spherical coordinates.  

*   **Answer** Compute Christoffel symbols by following equation
    
    \[latex\]\\eqalign{ \\vec{a}^i \\cdot \\frac{\\partial \\vec{a}\_j}{\\partial \\xi^k}=\\Gamma^i\_{jk} }\[/latex\].
    
    Every Christoffel symbol can be obtained.
    
    \[latex\]\\eqalign{ \\begin{aligned} &\\Gamma^1=\\begin{bmatrix}0 & 0& 0 \\\\0 & -r\\sin^2(\\phi)& 0 \\\\0 & 0& -r \\end{bmatrix}\\\\ \\\\ &\\Gamma^2=\\begin{bmatrix}0 & \\frac{1}{r}& 0 \\\\ \\frac{1}{r} & 0& \\cot\\phi \\\\0 & \\cot\\phi& 0 \\end{bmatrix}\\\\ \\\\ &\\Gamma^3=\\begin{bmatrix}0 & 0& \\frac{1}{r} \\\\0 & -\\cos \\phi \\sin \\phi& 0 \\\\\\frac{1}{r} & 0 & 0 \\end{bmatrix} \\end{aligned} }\[/latex\]
    

* * *

Question 2.c
------------

Express the continuity equation \[latex\] \\nabla \\cdot \\vec{v}=0 \[/latex\] in terms of physical velocity components \[latex\](v\_r ,\\ v\_\\theta ,\\ v\_\\phi ) \[/latex\].  

*   **Answer** The relation between covariant base vectors and physical vectors are
    
    \[latex\]\\eqalign{ \\left\\{ \\begin{aligned} &\\vec{a}\_1 = h\_1\\hat{e}\_r=\\sqrt{g\_{11}}\\hat{e}\_r=\\hat{e}\_r\\\\ &\\vec{a}\_2 = h\_2\\hat{e}\_\\theta=\\sqrt{g\_{22}}\\hat{e}\_\\theta=r\\hat{e}\_\\theta\\\\ &\\vec{a}\_3 = h\_3\\hat{e}\_\\phi=\\sqrt{g\_{22}}\\hat{e}\_\\phi=r\\sin\\theta\\hat{e}\_\\phi\\\\ \\end{aligned} \\right. }\[/latex\]
    
    Then, we can obtain the relation between contravariant components and physical components.
    
    \[latex\]\\eqalign{ \\left\\{ \\begin{aligned} &v^1 =v\_r\\\\ &v^2=\\frac{v\_\\theta}{r}\\\\ &v^3 = \\frac{v\_\\phi}{r sin\\theta}\\\\ \\end{aligned} \\right. }\[/latex\]
    
    The continuity equation in terms of physical velocity components can be derived as
    
    \[latex\] \\begin{aligned} \\nabla \\cdot \\vec{v}&=v^i\_{,j}=\\frac{\\partial v^i}{\\partial \\xi^i}+ \\Gamma^i\_{ni}v^i=\\frac{\\partial v^i}{\\partial \\xi^i}+\\frac{1} {J}\\frac{\\partial J}{\\partial \\xi^n}v^n\\\\ \\\\ &= \\frac{\\partial v^1}{\\partial r} + \\frac{\\partial v^2}{\\partial \\theta} + \\frac{\\partial v^3}{\\partial \\phi}+\\frac{1} {J}\\frac{\\partial J}{\\partial r}v^1+\\frac{1} {J}\\frac{\\partial J}{\\partial \\theta}v^2+\\frac{1} {J}\\frac{\\partial J}{\\partial \\phi}v^3\\\\ \\\\ &=\\frac{\\partial v\_r}{\\partial r} + \\frac{\\partial }{\\partial \\theta}\\left(\\frac{v\_\\theta}{r}\\right) + \\frac{\\partial}{\\partial \\phi}\\left(\\frac{v\_\\phi}{rsin\\theta}\\right) + \\frac{1} {r^2 sin\\theta}\\frac{\\partial (r^2 sin\\theta)}{\\partial r}v\_r +\\frac{1} {r^2 sin\\theta}\\frac{\\partial (r^2 sin\\theta)}{\\partial \\theta}\\frac{v\_\\theta}{r}\\\\ \\\\ & = \\frac{\\partial v\_r}{\\partial r} + \\frac{\\partial }{\\partial \\theta}\\left(\\frac{v\_\\theta}{r}\\right) + \\frac{\\partial}{\\partial \\phi}\\left(\\frac{v\_\\phi}{rsin\\theta}\\right) + \\frac{2}{r}v\_r +\\frac{cos\\theta} {r sin\\theta}v\_\\theta \\\\ \\\\ &= \\frac{1}{r^2}\\frac{\\partial \\left(r^2v\_r\\right)}{\\partial r}+\\frac{1}{r \\sin\\theta}\\frac{\\partial }{\\partial \\theta}\\left(\\sin\\theta\\ v\_\\theta\\right)+\\frac{1}{r\\sin \\theta}\\frac{\\partial v\_\\phi}{\\partial \\phi} \\end{aligned} \[/latex\]