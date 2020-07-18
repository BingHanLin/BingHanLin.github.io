---
title: MPS - MFS For Poisson Equation
tags:
  - Uncategorized
id: '224'
---

Governing & Boundary Equations
------------------------------

Governing equation (Poisson equation)

\[latex\]\\eqalign{  
\\nabla^2 u(x,y) = b(x,y)  
}\[/latex\]

Boundary condition (Dirichlet BC, first kind BC)

\[latex\]\\eqalign{  
u(x,y) = f(x,y)  
}\[/latex\]

* * *

MPS - MFS Method
----------------

A linear differential equation can be divided into two parts:

\[latex\]\\eqalign{  
u(x,y) = u\_p(x,y) + u\_h(x,y)  
}\[/latex\]

where \[latex\] u\_p(x,y) \[/latex\] is the particular solution and \[latex\] u\_h(x,y) \[/latex\] is the homogeneous solution.

*   **The particular solution :**

*   **The homogeneous solution :**

### Step1: Solve **Particular Solution**

Use the radial basis function (RBF) to interpolate the known function \[latex\] b(x,y)\[/latex\]:

\[latex\]\\eqalign{  
u(x,y) = u\_p(x,y) + u\_h(x,y)  
}\[/latex\]

### Step2: Solve **Homogeneous** **Solution**