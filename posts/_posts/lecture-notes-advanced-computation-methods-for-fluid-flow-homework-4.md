---
title: '[Lecture Notes] Advanced Computation Methods for Fluid Flow – Homework 4'
tags:
  - Advanced Computation Methods for Fluid Flow - 2018
  - computational fluid dynamics
  - numerical method
id: '777'
date: 2018-05-11 14:02:47
---

> _27/04/2018, Homework No. 4_

* * *

Question
--------

Consider the two-dimensional meandering channel shown in Figure:

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} &x=\\xi\\\\ &y=0.05\\left\[\\sin(5\\pi\\xi)+\\sin(\\pi\\eta)\\right\]\\\\ &z =\\zeta \\end{aligned} \\right. }\[/latex\]

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} &\\xi=\\xi^1=(\\overline{\\xi}-\\overline{\\xi}\_{min})/(\\overline{\\xi\_{max}}-\\overline{\\xi}\_{min}) \\\\ &\\eta=\\xi^2=(\\overline{\\eta}-\\overline{\\eta}\_{min})/(\\overline{\\eta\_{max}}-\\overline{\\eta}\_{min})-0.5 \\\\ &\\zeta=\\xi^3=(\\overline{\\zeta}-\\overline{\\zeta}\_{min})/(\\overline{\\zeta\_{max}}-\\overline{\\zeta}\_{min}) \\\\ \\end{aligned} \\right. }\[/latex\]

Express the following equations for incompressible flow in \[latex\] (\\xi ,\\eta , \\zeta)\[/latex\] coordinates in terms of partial derivatives of contravariant velocities \[latex\] (v^1 ,v^2 , v^3)\[/latex\]: (a) Continuity equation

\[latex\]\\eqalign{ v^i\_i=0 }\[/latex\]

(b) Navier-Stokes equations

\[latex\]\\eqalign{ \\rho\\left(\\frac{\\partial v^i}{\\partial t}+v^mv^i\_{,m}\\right)=\\rho f^i-g^{im}P\_{,m}+\\mu g^{mn}v^i\_{,mn} }\[/latex\]

![](https://bhlin.co.network/wp/wp-content/uploads/2018/04/擷取-1.png)

* * *

Answer
------

The covariant base vectors are obtained as follow

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} &\\vec{a}\_1= ( \\frac{\\partial \\xi }{\\partial \\xi },\\ \\frac{\\partial}{\\partial \\xi }\\left(0.05\\left\[\\sin(5\\pi\\xi)+\\sin(\\pi\\eta)\\right\]\\right),\\ \\frac{\\partial \\zeta }{\\partial \\xi }\\ )=(1,0.25\\pi \\cos(5\\pi\\xi),0) \\\\ &\\vec{a}\_2= ( \\frac{\\partial \\xi }{\\partial \\eta },\\ \\frac{\\partial}{\\partial \\eta }\\left(0.05\\left\[\\sin(5\\pi\\xi)+\\sin(\\pi\\eta)\\right\]\\right),\\ \\frac{\\partial \\zeta }{\\partial \\eta }\\ )=(0,0.05\\pi \\cos(5\\pi\\eta),0) \\\\ &\\vec{a}\_3= ( \\frac{\\partial \\xi }{\\partial \\zeta },\\ \\frac{\\partial}{\\partial \\zeta }\\left(0.05\\left\[\\sin(5\\pi\\xi)+\\sin(\\pi\\eta)\\right\]\\right),\\ \\frac{\\partial \\zeta }{\\partial \\zeta }\\ )=(0,0,1) \\end{aligned} \\right. }\[/latex\].

The jacobian of basis is

\[latex\] J=0.05\\pi \\cos(\\pi\\eta) \[/latex\].

The metric tensor \[latex\]g\_{ij}\[/latex\] and conjugate metric tensor \[latex\]g^{ij}\[/latex\] are found to be

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} & g\_{11}=1+\\frac{1}{16}\\pi^2 \\cos^2(5\\pi\\xi)\\\\ & g\_{22}=\\frac{1}{400}\\pi^2 \\cos^2(\\pi\\eta)\\\\ & g\_{33}=1\\\\ & g\_{12}=\\frac{1}{80}\\pi^2 \\cos(5\\pi\\xi)\\cos(\\pi\\eta)\\\\ & g\_{13}=0\\\\ & g\_{23}=0\\\\ \\end{aligned} \\right. }\[/latex\].

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} & g^{11}=1\\\\ & g^{22}=\\frac{25(16+\\pi^2\\cos^2(5\\pi\\xi))}{\\pi^2\\cos^2(\\pi\\eta)}\\\\ & g^{33}=1\\\\ & g^{12}=-5\\cos(5\\pi\\xi)\\sec(\\pi\\eta)\\\\ & g^{13}=0\\\\ & g^{23}=0\\\\ \\end{aligned} \\right. }\[/latex\].

The christoffel symbol \[latex\]\\Gamma^i\_{jk}\[/latex\] is calculated.

\[latex\]\\eqalign{ \\begin{aligned} &\\Gamma^1=\\begin{bmatrix}0 & 0& 0 \\\\0 & 0& 0 \\\\0 & 0& 0 \\\\ \\end{bmatrix} \\\\ \\\\ &\\Gamma^2=\\begin{bmatrix}-25\\pi \\frac{\\sin(5\\pi\\xi)}{\\cos(\\pi\\eta)} & 0& 0 \\\\0 & -\\pi \\tan(\\pi\\eta)& 0 \\\\0 & 0& 0 \\end{bmatrix}\\\\ \\\\ &\\Gamma^3=\\begin{bmatrix}0 & 0& 0 \\\\0 & 0& 0 \\\\0 & 0& 0 \\\\ \\end{bmatrix} \\end{aligned} }\[/latex\].

### Answer (a)

\[latex\]\\eqalign{ \\begin{aligned} v^i\_{,i} &=\\frac{\\partial v^1}{\\partial \\xi^1}+\\frac{\\partial v^2}{\\partial \\xi^2}+\\frac{\\partial v^3}{\\partial \\xi^3}+ \\Gamma^1\_{n1}v^n+\\Gamma^2\_{n2}v^n+\\Gamma^3\_{n3}v^n\\\\ \\\\ &=\\frac{\\partial v^1}{\\partial \\xi^1}+\\frac{\\partial v^2}{\\partial \\xi^2}+\\frac{\\partial v^3}{\\partial \\xi^3}-\\pi \\tan(\\pi\\eta)v^2\\\\ \\end{aligned} }\[/latex\].

### Answer (b)

The diffusion term on the right hand side can be expanded

\[latex\]\\eqalign{ \\mu g^{mn}v^i\_{,mn}&=\\mu g^{mn} D^i\_{m,n}\\\\ &=\\mu g^{mn} \\left(\\frac{\\partial D^i\_m}{\\partial \\xi^n}+\\Gamma^i\_{kn} D^k\_m-\\Gamma^k\_{mn} D^i\_k\\right)\\\\ &=\\mu g^{mn} \\left\[\\frac{\\partial}{\\partial \\xi^n}\\left(\\frac{\\partial v^i}{\\partial \\xi^m}+\\Gamma^i\_{km}v^k\\right)+\\Gamma^i\_{kn} \\left(\\frac{\\partial v^k}{\\partial \\xi^m}+\\Gamma^k\_{pm}v^p\\right)-\\Gamma^k\_{mn} \\left(\\frac{\\partial v^i}{\\partial \\xi^k}+\\Gamma^i\_{pk}v^p\\right)\\right\]\\\\ &=\\mu g^{mn} \\left\[\\frac{\\partial}{\\partial \\xi^n}\\left(\\frac{\\partial v^i}{\\partial \\xi^m}+\\Gamma^i\_{pm}v^p\\right)+\\Gamma^i\_{kn} \\left(\\frac{\\partial v^k}{\\partial \\xi^m}+\\Gamma^k\_{pm}v^p\\right)-\\Gamma^k\_{mn} \\left(\\frac{\\partial v^i}{\\partial \\xi^k}+\\Gamma^i\_{pk}v^p\\right)\\right\]\\\\ }\[/latex\].

Then derivative Navier-Stokes equations as

\[latex\]\\eqalign{ &\\rho\\left(\\frac{\\partial v^i}{\\partial t}+v^mv^i\_{,m}\\right)=\\rho f^i-g^{im}P\_{,m}+\\mu g^{mn}v^i\_{,mn} \\\\ \\\\ \\Rightarrow&\\rho\\frac{\\partial v^i}{\\partial t}+\\rho v^m\\left(\\frac{\\partial v^i}{\\partial \\xi^m}+\\Gamma^i\_{km}v^k\\right)=\\rho f^i+g^{im}\\frac{\\partial P}{\\partial \\xi^m}+\\mu g^{mn} D^i\_{m,n}\\\\ \\\\ \\Rightarrow&\\rho\\frac{\\partial v^i}{\\partial t}+\\rho v^m\\left(\\frac{\\partial v^i}{\\partial \\xi^m}+\\Gamma^i\_{km}v^k\\right)=\\rho f^i+g^{im}\\frac{\\partial P}{\\partial \\xi^m}+\\\\ &\\qquad \\mu g^{mn} \\left\[\\frac{\\partial}{\\partial \\xi^n}\\left(\\frac{\\partial v^i}{\\partial \\xi^m}+\\Gamma^i\_{pm}v^p\\right)+\\Gamma^i\_{kn} \\left(\\frac{\\partial v^k}{\\partial \\xi^m}+\\Gamma^k\_{pm}v^p\\right)-\\Gamma^k\_{mn} \\left(\\frac{\\partial v^i}{\\partial \\xi^k}+\\Gamma^i\_{pk}v^p\\right)\\right\] }\[/latex\].

* * *

**In \[latex\]\\xi^1\[/latex\] direction:**

\[latex\]\\eqalign{ \\rho\\frac{\\partial v^1}{\\partial t}+\\rho\\left(v^1\\frac{\\partial v^1}{\\partial \\xi^1}+v^2\\frac{\\partial v^1}{\\partial \\xi^2}+v^3\\frac{\\partial v^1}{\\partial \\xi^3}\\right)&=\\rho f^1+g^{11}\\frac{\\partial P}{\\partial \\xi^1}+g^{12}\\frac{\\partial P}{\\partial \\xi^2}\\\\ &+\\mu\\left(g^{11} \\frac{\\partial^2v^1}{\\partial \\xi^1\\partial \\xi^1}+g^{22} \\frac{\\partial^2v^1}{\\partial \\xi^2\\partial \\xi^2}+g^{33} \\frac{\\partial^2v^1}{\\partial \\xi^3\\partial \\xi^3}+2g^{12} \\frac{\\partial^2v^1}{\\partial \\xi^1\\partial \\xi^2}\\right)\\\\ &-\\mu\\left( g^{11}\\Gamma^2\_{11}\\frac{\\partial v^1}{\\partial \\xi^2}+g^{22}\\Gamma^2\_{22}\\frac{\\partial v^1}{\\partial \\xi^2} \\right)\\\\ }\[/latex\].

\[latex\]\\eqalign{ \\rho\\frac{\\partial v^1}{\\partial t}+&\\rho\\left(v^1\\frac{\\partial v^1}{\\partial \\xi^1}+v^2\\frac{\\partial v^1}{\\partial \\xi^2}+v^3\\frac{\\partial v^1}{\\partial \\xi^3}\\right)\\\\ &=\\rho f^1+\\frac{\\partial P}{\\partial \\xi^1}-5\\frac{\\cos(5\\pi\\xi)}{\\cos(\\pi\\eta)}\\frac{\\partial P}{\\partial \\xi^2}\\\\ &+\\mu\\left( \\frac{\\partial^2v^1}{\\partial \\xi^1\\partial \\xi^1}+\\frac{25(16+\\pi^2\\cos^2(5\\pi\\xi))}{\\pi^2\\cos^2(\\pi\\eta)} \\frac{\\partial^2v^1}{\\partial \\xi^2\\partial \\xi^2}+ \\frac{\\partial^2v^1}{\\partial \\xi^3\\partial \\xi^3}-10\\frac{\\cos(5\\pi\\xi)}{\\cos(\\pi\\eta)} \\frac{\\partial^2v^1}{\\partial \\xi^1\\partial \\xi^2}\\right)\\\\ &-\\mu\\left( -25\\pi \\frac{\\sin(5\\pi\\xi)}{\\cos(\\pi\\eta)}\\frac{\\partial v^1}{\\partial \\xi^2}-\\frac{25(16+\\pi^2\\cos^2(5\\pi\\xi))}{\\pi\\cos^2(\\pi\\eta)} \\tan(\\pi\\eta)\\frac{\\partial v^1}{\\partial \\xi^2} \\right)\\\\ }\[/latex\].

* * *

**In \[latex\]\\xi^2\[/latex\] direction:**

\[latex\]\\eqalign{ \\rho\\frac{\\partial v^2}{\\partial t}+&\\rho\\left(v^1\\frac{\\partial v^2}{\\partial \\xi^1}+v^2\\frac{\\partial v^2}{\\partial \\xi^2}+v^3\\frac{\\partial v^2}{\\partial \\xi^3}+v^1\\Gamma^2\_{11}v^1+v^2\\Gamma^2\_{22}v^2\\right)\\\\ &=\\rho f^2+g^{21}\\frac{\\partial P}{\\partial \\xi^1}+g^{22}\\frac{\\partial P}{\\partial \\xi^2}+g^{23}\\frac{\\partial P}{\\partial \\xi^3}\\\\ &+\\mu\\left(g^{11} \\frac{\\partial^2v^2}{\\partial \\xi^1\\partial \\xi^1}+g^{22} \\frac{\\partial^2v^2}{\\partial \\xi^2\\partial \\xi^2}+g^{33} \\frac{\\partial^2v^2}{\\partial \\xi^3\\partial \\xi^3}+2g^{12} \\frac{\\partial^2v^2}{\\partial \\xi^1\\partial \\xi^2}\\right)\\\\ &+\\mu\\left(g^{11}\\frac{\\partial}{\\partial\\xi^1}(\\Gamma^2\_{11}v^1)+g^{12}\\frac{\\partial}{\\partial\\xi^2}(\\Gamma^2\_{11}v^1)+g^{21}\\frac{\\partial}{\\partial\\xi^1}(\\Gamma^2\_{22}v^2)+g^{22}\\frac{\\partial}{\\partial\\xi^2}(\\Gamma^2\_{22}v^2)\\right)\\\\ &+\\mu\\left( g^{11}\\Gamma^2\_{11}\\frac{\\partial v^1}{\\partial \\xi^1}+g^{21}\\Gamma^2\_{11}\\frac{\\partial v^1}{\\partial \\xi^2}+g^{12}\\Gamma^2\_{22}\\frac{\\partial v^2}{\\partial \\xi^1}\\right)\\\\ &+\\mu\\left( g^{12}\\Gamma^2\_{22}\\Gamma^2\_{11}v^1-g^{11}\\Gamma^2\_{11}\\frac{\\partial v^2}{\\partial \\xi^2} -g^{11}\\Gamma^2\_{22}\\Gamma^2\_{11}v^2\\right)\\\\ }\[/latex\].

\[latex\]\\eqalign{ \\rho\\frac{\\partial v^2}{\\partial t}+&\\rho\\left(v^1\\frac{\\partial v^2}{\\partial \\xi^1}+v^2\\frac{\\partial v^2}{\\partial \\xi^2}+v^3\\frac{\\partial v^2}{\\partial \\xi^3}-25\\pi \\frac{\\sin(5\\pi\\xi)}{\\cos(\\pi\\eta)}v^1v^1-\\pi \\tan(\\pi\\eta)v^2v^2\\right)\\\\ &=\\rho f^2-5\\cos(5\\pi\\xi)\\sec(\\pi\\eta)\\frac{\\partial P}{\\partial \\xi^1}+\\frac{25(16+\\pi^2\\cos^2(5\\pi\\xi))}{\\pi^2\\cos^2(\\pi\\eta)}\\frac{\\partial P}{\\partial \\xi^2}\\\\ &+\\mu\\left( \\frac{\\partial^2v^2}{\\partial \\xi^1\\partial \\xi^1}+\\frac{25(16+\\pi^2\\cos^2(5\\pi\\xi))}{\\pi^2\\cos^2(\\pi\\eta)} \\frac{\\partial^2v^2}{\\partial \\xi^2\\partial \\xi^2}+ \\frac{\\partial^2v^2}{\\partial \\xi^3\\partial \\xi^3}-10\\frac{\\cos(5\\pi\\xi)}{\\cos(\\pi\\eta)} \\frac{\\partial^2v^2}{\\partial \\xi^1\\partial \\xi^2}\\right)\\\\ &+\\mu\\left(\\frac{\\partial}{\\partial\\xi^1}(-25\\pi \\frac{\\sin(5\\pi\\xi)}{\\cos(\\pi\\eta)}v^1)-5\\frac{\\cos(5\\pi\\xi)}{\\cos(\\pi\\eta)}\\frac{\\partial}{\\partial\\xi^2}(-25\\pi \\frac{\\sin(5\\pi\\xi)}{\\cos(\\pi\\eta)}v^1)\\right)\\\\ &+\\mu\\left(-5\\frac{\\cos(5\\pi\\xi)}{\\cos(\\pi\\eta)}\\frac{\\partial}{\\partial\\xi^1}(-\\pi \\tan(\\pi\\eta)v^2)+\\frac{25(16+\\pi^2\\cos^2(5\\pi\\xi))}{\\pi^2\\cos^2(\\pi\\eta)}\\frac{\\partial}{\\partial\\xi^2}(-\\pi \\tan(\\pi\\eta)v^2)\\right)\\\\ &+\\mu\\left( -25\\pi \\frac{\\sin(5\\pi\\xi)}{\\cos(\\pi\\eta)}\\frac{\\partial v^1}{\\partial \\xi^1}+75\\frac{\\cos(5\\pi\\xi)}{\\cos(\\pi\\eta)}\\pi \\frac{\\sin(5\\pi\\xi)}{\\cos(\\pi\\eta)}\\frac{\\partial v^1}{\\partial \\xi^2}-5\\frac{\\cos(5\\pi\\xi)}{\\cos(\\pi\\eta)}\\pi \\tan(\\pi\\eta)\\frac{\\partial v^2}{\\partial \\xi^1}\\right)\\\\ &+\\mu\\left( -75\\frac{\\cos(5\\pi\\xi)}{\\cos(\\pi\\eta)}\\pi \\tan(\\pi\\eta)\\pi \\frac{\\sin(5\\pi\\xi)}{\\cos(\\pi\\eta)}v^1+25\\pi \\frac{\\sin(5\\pi\\xi)}{\\cos(\\pi\\eta)}\\frac{\\partial v^2}{\\partial \\xi^2} -25\\pi \\tan(\\pi\\eta)\\pi \\frac{\\sin(5\\pi\\xi)}{\\cos(\\pi\\eta)}v^2\\right)\\\\ }\[/latex\].

* * *

**In \[latex\]\\xi^3\[/latex\] direction:**

\[latex\]\\eqalign{ \\rho\\frac{\\partial v^3}{\\partial t}+\\rho\\left(v^1\\frac{\\partial v^3}{\\partial \\xi^1}+v^2\\frac{\\partial v^3}{\\partial \\xi^2}+v^3\\frac{\\partial v^3}{\\partial \\xi^3}\\right)&=\\rho f^3+g^{31}\\frac{\\partial P}{\\partial \\xi^1}+g^{32}\\frac{\\partial P}{\\partial \\xi^2}+g^{33}\\frac{\\partial P}{\\partial \\xi^3}\\\\ &+\\mu\\left(g^{11} \\frac{\\partial^2v^3}{\\partial \\xi^1\\partial \\xi^1}+g^{22} \\frac{\\partial^2v^3}{\\partial \\xi^2\\partial \\xi^2}+g^{33} \\frac{\\partial^2v^3}{\\partial \\xi^3\\partial \\xi^3}+2g^{12} \\frac{\\partial^2v^3}{\\partial \\xi^1\\partial \\xi^2}\\right)\\\\ &-\\mu\\left( g^{11}\\Gamma^2\_{11}\\frac{\\partial v^3}{\\partial \\xi^2}+g^{22}\\Gamma^2\_{22}\\frac{\\partial v^3}{\\partial \\xi^2} \\right)\\\\ }\[/latex\].

\[latex\]\\eqalign{ \\rho\\frac{\\partial v^3}{\\partial t}+&\\rho\\left(v^1\\frac{\\partial v^3}{\\partial \\xi^1}+v^2\\frac{\\partial v^3}{\\partial \\xi^2}+v^3\\frac{\\partial v^3}{\\partial \\xi^3}\\right)\\\\ &=\\rho f^3+\\frac{\\partial P}{\\partial \\xi^3}\\\\ &+\\mu\\left( \\frac{\\partial^2v^3}{\\partial \\xi^1\\partial \\xi^1}+\\frac{25(16+\\pi^2\\cos^2(5\\pi\\xi))}{\\pi^2\\cos^2(\\pi\\eta)} \\frac{\\partial^2v^3}{\\partial \\xi^2\\partial \\xi^2}+ \\frac{\\partial^2v^3}{\\partial \\xi^3\\partial \\xi^3}-10\\frac{\\cos(5\\pi\\xi)}{\\cos(\\pi\\eta)}\\frac{\\partial^2v^3}{\\partial \\xi^1\\partial \\xi^2}\\right)\\\\ &-\\mu\\left( -25\\pi \\frac{\\sin(5\\pi\\xi)}{\\cos(\\pi\\eta)}\\frac{\\partial v^3}{\\partial \\xi^2}-\\frac{25(16+\\pi^2\\cos^2(5\\pi\\xi))}{\\pi\\cos^2(\\pi\\eta)} \\tan(\\pi\\eta)\\frac{\\partial v^3}{\\partial \\xi^2} \\right)\\\\ }\[/latex\].