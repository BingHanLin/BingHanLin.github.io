---
title: Vorticity – Stream function (Lid-driven cavity problem)
tags:
  - computational fluid dynamics
  - Computational Fluid Dynamics (CFD)
  - python
id: '150'
date: 2018-03-19 23:30:53
---

Vorticity – Stream function
---------------------------

The stream function-vorticity formulation is one of the algorithms for solving unsteady, incompressible Navier-Stokes problems. For incompressible flows with constant fluid properties, the Navier–Stokes equations can be simplified by two dependent variables which are stream function \[latex\] \\psi \[/latex\] and vorticity  \[latex\] \\omega \[/latex\]. Consider two-dimensional flow in x-y plane, the vorticity at a point can be defined as

\[latex\]\\eqalign{\\omega\_z=\\frac{\\partial v}{\\partial x}-\\frac{\\partial u}{\\partial y} }\[/latex\]

Next, a scalar function is defined in such a way that makes velocity components satisfy the continuity equation ( \[latex\] \\frac{\\partial u}{\\partial x}+\\frac{\\partial v}{\\partial y}=0 \[/latex\] ). Such a function is known as the stream function, and is given by,

\[latex\]\\eqalign{\\bf V=\\nabla\\times \\psi }\[/latex\]

where \[latex\]\\bf V \[/latex\] is the velocity vector. In Cartesian coordinate system, the relation between velocity compoenents and stream function becomes

\[latex\]\\eqalign{u=\\frac{\\partial \\psi}{y} ,\\quad v=-\\frac{\\partial \\psi}{x}}\[/latex\]

Now, a equation connecting the streamfunction and the vorticity can be obtained by substituting the velocity components, in terms of stream function. Thus, we have

\[latex\]\\eqalign{\\nabla^2\\psi=-\\omega\_z}\[/latex\]

Finally, by taking the curl of the general Navier–Stokes equation, we obtain the following Helmholtz equation:

\[latex\]\\eqalign{\\frac{\\partial \\omega\_z}{\\partial t}+ \\bf{V}\\cdot\\nabla\\omega\_z=\\nu \\nabla^2 \\omega\_z }\[/latex\]

This parabolic PDE is called the vorticity transport equation. Since we have found an equation for ω, the of stream function that automatically produces divergence-free velocity fields can be solved.

* * *

Vorticity – Stream function governing equation in cartesian coordinate
----------------------------------------------------------------------

The above equations are then described in cylindrical coordinates(r-z system) as follow,

\[latex\]\\eqalign{\\frac{\\partial^2 \\psi}{\\partial x^2}+ \\frac{\\partial^2 \\psi}{\\partial y^2} - \\omega ,}\[/latex\] \[latex\]\\eqalign{\\frac{\\partial \\omega}{\\partial t}+u\\frac{\\partial \\omega}{\\partial x}+v\\frac{\\partial \\omega}{\\partial y}= \\nu\\left(\\frac{\\partial^2 \\omega}{\\partial x^2}+ \\frac{\\partial^2 \\omega}{\\partial y^2}\\right)} \[/latex\]

where

\[latex\]\\eqalign{ u = \\frac{\\partial \\psi}{\\partial x},}\[/latex\] \[latex\]\\eqalign{v = -\\frac{\\partial \\psi}{\\partial y},}\[/latex\] \[latex\]\\eqalign{ \\omega= \\omega\_z=\\frac{\\partial v}{\\partial x}-\\frac{\\partial u}{\\partial y} .}\[/latex\]

Thus, the Navier–Stokes equations in cylinderical coordinates have been replaced by a set of two partial differential equations.

* * *

Case : Lid-driven cavity problem
--------------------------------

Lid-driven cavity problem has been used as a validation case for numerical methods. The formulations above are approached by finite difference method. The problem geometry is simple and two-dimensional, and the boundary conditions are also simple. The standard case is fluid contained in a square domain with Dirichlet boundary conditions on all sides, with three stationary sides and one moving side (with unit velocity in x direction).

![Alt text](http://bhlin.comli.com/wp-content/uploads/2017/09/lid-driven-cavity_schematic-diagram-1024x698.png) _sketch of the computational domain and boundary._

As usual, the program written in python is attached here: [**my github**](https://github.com/BingHanLin/Vorticity-Stream-function-Solver). The case with Reynolds number equal to 10 is presented here. The fluid velocity field is visualized at 10 seconds in the figure. The black arrows are velocity vectors and the contour of vorticity is plotted in the background.

![Alt text](http://bhlin.comli.com/wp-content/uploads/2017/09/quiver-plot.png) _Lid driven cavity velocity vector and contour of vorticity with Re=10._

* * *

*   Reference:

1.  [ON THE DOWNSTREAM BOUNDARY CONDITIONS FOR THE VORTICITY-STREAM FUNCTION FORMULATION OF TWO-DIMENSIONAL INCOMPRESSIBLE FLOWS](http://www.tafsm.org/PUB_PRE/jALL/j21-CMAME-OBC.pdf)
2.  [Streamfunction-Vorticity Formulation](https://www.iist.ac.in/sites/default/files/people/psi-omega.pdf)
3.  [A Finite Difference Code for the Navier-Stokes Equations in Vorticity/ Streamfunction Form](https://www3.nd.edu/~gtryggva/CFD-Course/2011-Lecture-5.pdf)