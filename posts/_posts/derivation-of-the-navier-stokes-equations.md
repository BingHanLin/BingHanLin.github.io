---
title: Derivation of the Navier–Stokes equations
tags:
  - Computational Fluid Dynamics (CFD)
id: '1699'
date: 2019-06-26 16:23:07
---

Assumption
----------

In this post, we apply some assumptions into our derivation process:

*   Newtonian fluid
*   Incompressible flow

* * *

Reynolds Transport Theorem
--------------------------

![](https://bhlin.co.network/wp/wp-content/uploads/2019/05/MV-CV-1024x694.png)

Material Volume and Control Volume moving over time.

Here, we obtain the **Reynolds Transport Theorem** which provides the conversion formulation between **Lagrangian description (LHS)** and **Eulerian description (RHS)**.

\[latex\]\\eqalign{\\frac{D}{Dt}\\int\\limits\_{MV(t)}F(\\vec{\\mathrm{r}},t)\\mathrm{d}\\Omega=\\frac{d}{dt}\\int\\limits\_{CV(t)}F(\\vec{\\mathrm{r}},t) \\ \\mathrm{d}\\Omega + \\oint\\limits\_{CS(t)}F(\\vec{\\mathrm{r}},t)\\vec{V}\\cdot \\vec{n}\\ \\mathrm{d}S}\[/latex\]

Where the subscript **MV** indicates material volume, **CV** indicates control volume, and **CS** is control surface.

Further apply **divergence theorem** ( \[latex\]\\int\\vec{\\mathrm{A}} \\cdot \\vec{n} \\ \\mathrm{d}S=\\int\\nabla \\cdot \\vec{\\mathrm{A}} \\ \\mathrm{d}\\Omega\[/latex\] ) to convert surface integrals in above equation into volume integrals. This gives us an equation as follow.

\[latex\]\\eqalign{\\frac{D}{Dt}\\int\\limits\_{MV}F\\mathrm{d}\\Omega=\\frac{d}{dt}\\int\\limits\_{CV}F \\ \\mathrm{d}\\Omega + \\int\\limits\_{  
CV }\\nabla\\cdot (  
F \\vec{V})\\ \\mathrm{d}  
\\Omega}\[/latex\]

The terms in **Eulerian description (RHS)** become volume integrals now. Let \[latex\] F = \\rho \\ \\phi \[/latex\], then we have,

\[latex\]\\eqalign{ \\frac{D}{Dt}\\int\\limits\_{MV}\\rho \\ \\phi\\ \\mathrm{d}\\Omega=\\frac{d}{dt}\\int\\limits\_{CV} \\rho \\ \\phi\\ \\mathrm{d}\\Omega + \\int\\limits\_{CV}  
\\nabla\\cdot (  
\\rho \\ \\phi \\vec{V})\\ \\mathrm{d}\\Omega\\\\ }\[/latex\]

When we further consider the arbitrary (shape and size) but **fixed control volume (independent of time)**, we have the constraint:

\[latex\]\\eqalign{ \\frac{d}{dt}\\int\\limits\_{CV}F\\mathrm{d}\\Omega = \\int\\limits\_{CV}\\frac{\\partial F}{\\partial t}\\mathrm{d}\\Omega }\[/latex\]

Take the constraint into the equation above gives us:

\[latex\] \\eqalign{ &\\frac{D}{Dt}\\int\\limits\_{MV}F\\mathrm{d}\\Omega = \\int\\limits\_{CV}\\left\[ \\frac{\\partial F}{\\partial t}+\\nabla \\cdot(F\\vec{V})\\right\]\\mathrm{d}\\Omega \\\\  
&because, \\quad \\nabla \\cdot(F\\vec{V})=\\vec{V}\\cdot\\nabla F+F\\nabla\\cdot\\vec{V}\\\\  
&therefore, \\quad \\frac{\\partial F}{\\partial t}+\\nabla \\cdot(F\\vec{V})= \\left(\\frac{\\partial F}{\\partial t}+\\vec{V}\\cdot\\nabla F\\right)+F\\nabla\\cdot\\vec{V}=\\frac{DF}{Dt}+F\\nabla\\cdot\\vec{V}\\\\  
&finally, \\quad \\frac{D}{Dt}\\int\\limits\_{MV}F\\mathrm{d}\\Omega = \\int\\limits\_{CV}\\frac{DF}{Dt}\\mathrm{d}\\Omega+\\int\\limits\_{CV} F\\nabla\\cdot\\vec{V}\\mathrm{d}\\Omega \\\\  
&and,\\quad \\frac{D}{Dt}\\int\\limits\_{MV}\\rho\\phi\\mathrm{d}\\Omega = \\int\\limits\_{CV}\\frac{D(\\rho\\phi)}{Dt}\\mathrm{d}\\Omega+\\int\\limits\_{CV} \\rho\\phi\\nabla\\cdot\\vec{V}\\mathrm{d}\\Omega }  
\[/latex\]

Accordingly, we obtain the form of **Reynolds Transport Theorem** within the **fixed control volume**. 

* * *

Conservation of Mass
--------------------

Let \[latex\]\\phi=1\[/latex\], the mass \[latex\]m\[/latex\] can be represented as

\[latex\] \\eqalign{  
m =\\int\\limits\_{MV}\\rho\\ \\mathrm{d}\\Omega  
} \[/latex\]

In the Lagrangian description, the equation for conservation of mass is written as,

\[latex\]\\eqalign{  
\\frac{Dm}{Dt} =\\frac{D}{Dt}\\int\\limits\_{MV}\\rho\\ \\mathrm{d}\\Omega=0 \\ .  
}\[/latex\]

For arbitrary, but fixed control volume, we have the following equation.

\[latex\] \\eqalign{ \\frac{D}{Dt}\\int\\limits\_{MV}\\rho \\mathrm{d}\\Omega&  
\=\\frac{d}{dt}\\int\\limits\_{CV} \\rho \\mathrm{d}\\Omega + \\int\\limits\_{CV}  
\\nabla\\cdot (  
\\rho \\vec{V})\\ \\mathrm{d}\\Omega\\\\  
&  
\=\\int\\limits\_{CV} \\frac{\\partial \\rho}{\\partial t} \\mathrm{d}\\Omega + \\int\\limits\_{CV}  
\\nabla\\cdot (  
\\rho \\vec{V})\\ \\mathrm{d}\\Omega\\\\  
&  
\=\\int\\limits\_{CV} \\left\[\\frac{\\partial \\rho}{\\partial t} +  
\\nabla\\cdot (  
\\rho \\vec{V})\\ \\right\]\\mathrm{d}\\Omega  
\=0 }  
\[/latex\]

Now, we have the **differential form** of the continuity equation in eulerian description.

\[latex\] \\eqalign{  
\\frac{\\partial \\rho}{\\partial t} +  
\\nabla\\cdot (  
\\rho \\vec{V})=\\frac{\\partial \\rho}{\\partial t} + \\rho(  
\\nabla\\cdot\\vec{V} ) +  
\\vec{V}\\cdot (  
\\nabla\\rho )=0 } \[/latex\]

### Incompressible flow

Consider the incompressible flow (density \[latex\]\\rho\[/latex\] of a certain fluid parcel does not change as a function of time) in our applications, we have the following equation.

\[latex\] \\eqalign{ \\underset{ Lagrangian }{ \\frac{D\\rho}{Dt} } =  
\\underset{ Eulerian }{  
\\frac{\\partial \\rho}{\\partial t}+\\vec{V}\\cdot\\nabla\\rho} =0}  
\[/latex\]

Compare the difference between the **differential form** of continuity equation and equation of incompressible flow condition, we have:

\[latex\] \\eqalign{ \\nabla \\cdot \\vec{V}=0 }  
\[/latex\]

Here we obtain the **continuity equation** for the **incompressible flow**.

* * *

Conservation of Momentum
------------------------

Let \[latex\]\\phi=\\vec{V}\[/latex\], the momentum \[latex\]\\vec{M}\[/latex\] can be represented as

\[latex\] \\eqalign{ \\vec{M} =\\int\\limits\_{MV}\\rho \\vec{V} \\mathrm{d}\\Omega } \[/latex\]

In the Lagrangian description, the equation for conservation of momentum is written as,

\[latex\] \\eqalign{ \\underset{Rate \\ of \\ change \\ of \\ momentum \\ in \\ MV}{\\frac{D}{Dt}\\int\\limits\_{MV}\\vec{V}\\rho \\ \\mathrm{d}\\Omega}=\\underset{ Body \\ force}{\\int\\limits\_{MV}\\vec{f}\\rho \\ \\mathrm{d}\\Omega}+\\underset{ Surface \\ force}{\\int\\limits\_{MS}\\overline{\\overline{T}}\\cdot \\vec{n}\\mathrm{d}S} }  
\[/latex\]

Where \[latex\] \\overline{\\overline{T}}\\cdot \\vec{n} = \\vec{n} \\cdot \\overline{\\overline{T}} \[/latex\] is surface force, \[latex\] \\overline{\\overline{T}} \[/latex\] is the stress tensor, and \[latex\] \\vec{f}\[/latex\] indicates the body force.

Use Reynolds transport theorem to transfer the equation above into the following equation:

\[latex\] \\eqalign{ {\\frac{d}{dt}\\int\\limits\_{CV}\\vec{V}\\rho \\ \\mathrm{d}\\Omega}+\\int\\limits\_{CS} \\vec{V} \\rho \\vec{V}\\cdot \\vec{n}\\mathrm{d}S={\\int\\limits\_{CV}\\vec{f}\\rho \\ \\mathrm{d}\\Omega}+{\\int\\limits\_{CS}\\overline{\\overline{T}}\\cdot \\vec{n}\\mathrm{d}S} }\[/latex\]

Again, we apply **divergence theorem** ( \[latex\]\\int\\vec{\\mathrm{A}} \\cdot \\vec{n} \\ \\mathrm{d}S=\\int\\nabla \\cdot \\vec{\\mathrm{A}} \\ \\mathrm{d}\\Omega\[/latex\] ) on both side of the equation.

\[latex\] \\eqalign{ {\\frac{d}{dt}\\int\\limits\_{CV}\\vec{V}\\rho \\ \\mathrm{d}\\Omega}+\\int\\limits\_{CV} \\nabla\\cdot(\\vec{V} \\rho \\vec{V})\\mathrm{d}\\Omega={\\int\\limits\_{CV}\\vec{f}\\rho \\ \\mathrm{d}\\Omega}+{\\int\\limits\_{CV}\\nabla\\cdot\\overline{\\overline{T}}\\mathrm{d}\\Omega}} \[/latex\]

For arbitrary, but fixed control volume, we have the following equation.

\[latex\] \\eqalign{ {\\int\\limits\_{CV}\\frac{\\partial}{\\partial t}(\\rho\\vec{V}) \\ \\mathrm{d}\\Omega}+\\int\\limits\_{CV} \\nabla\\cdot(\\rho\\vec{V} \\vec{V})\\mathrm{d}\\Omega={\\int\\limits\_{CV} \\rho \\vec{f} \\ \\mathrm{d}\\Omega}+{\\int\\limits\_{CV}\\nabla\\cdot\\overline{\\overline{T}}\\mathrm{d}\\Omega}} \[/latex\]

and thus,

\[latex\] \\eqalign{ {\\int\\limits\_{CV}\\left\[\\frac{\\partial}{\\partial t}(\\rho\\vec{V}) +\\nabla\\cdot(\\rho\\vec{V} \\vec{V})  
\-\\rho\\vec{f}  
\-\\nabla\\cdot\\overline{\\overline{T}}  
\\right\]\\ \\mathrm{d}\\Omega}=0 }\[/latex\]

Now, we have the **differential form** of the momentum Equations in eulerian description (not restricted to Newtonian fluid).

\[latex\] \\eqalign{ \\frac{\\partial}{\\partial t}(\\rho\\vec{V}) +\\nabla\\cdot(\\rho\\vec{V} \\vec{V})  
\=\\rho\\vec{f}  
+\\nabla\\cdot\\overline{\\overline{T}} }\[/latex\]

### Newtonian fluid

The stress tensor can be expressed as the sum of two stress tensors, namely: the **hydrostatic stress tensor** and the **deviatoric stress tensor**. Thus, \[latex\] \\overline{\\overline{T}} \[/latex\] is broken down into

\[latex\] \\eqalign{ \\overline{\\overline{T}} =T\_{ij}= -p\\delta\_{ij}+\\tau\_{ij} }\[/latex\]

The second part is called the **deviatoric stress tensor**. For a **Newtonian Fluid**, the deviatoric stress tensor is proportional to the rate of deformation (the change in velocity in the directions of the stress).

\[latex\] \\eqalign{ \\tau\_{ij} = \\mu\\left( \\frac{\\partial u\_i}{\\partial x\_j}+\\frac{\\partial u\_j}{\\partial x\_i}\\right)+\\lambda\\frac{\\partial u\_k}{\\partial x\_k}\\delta\_{ij} }\[/latex\]

The total stress tensor \[latex\] \\overline{\\overline{T}} \[/latex\] is therefore

\[latex\] \\eqalign{ T\_{ij} = \\left(-p+\\lambda\\frac{\\partial u\_k}{\\partial x\_k}\\right)\\delta\_{ij}+\\mu\\left( \\frac{\\partial u\_i}{\\partial x\_j}+\\frac{\\partial u\_j}{\\partial x\_i}\\right) }\[/latex\] .

In the vector form

\[latex\] \\eqalign{ \\overline{\\overline{T}} = \\left(-p+\\lambda\\nabla \\cdot\\vec{V}\\right)\\overline{\\overline{I}}+2\\mu\\overline{\\overline{D}} }\[/latex\] ,

where \[latex\] \\overline{\\overline{D}}=D\_{ij}= \\frac{1}{2}\\left( \\frac{\\partial u\_i}{\\partial x\_j}+\\frac{\\partial u\_j}{\\partial x\_i}\\right) \[/latex\].

Substituting this into the previous equation, we arrive at the momentum equation for a Newtonian fluid:

\[latex\] \\eqalign{  
\\frac{\\partial}{\\partial t}(\\rho\\vec{V}) +\\nabla\\cdot(\\rho\\vec{V} \\vec{V})  
\=\\rho\\vec{f}  
\-\\nabla p  
+\\left(\\mu+\\lambda\\right)\\nabla\\left(\\nabla \\cdot \\vec{V}\\right)  
+\\mu\\nabla^2\\vec{V}  
} \[/latex\] .

### Incompressible flow

Consider the incompressible flow (\[latex\] \\nabla \\cdot \\vec{V}=0 \[/latex\]) in our applications, we have the following equation.

\[latex\] \\eqalign{  
\\frac{\\partial}{\\partial t}(\\rho\\vec{V}) +\\nabla\\cdot(\\rho\\vec{V} \\vec{V})  
\=\\rho\\vec{f}  
\-\\nabla p  
+\\mu\\nabla^2\\vec{V}  
} \[/latex\]

Here we obtain the **momentum equation** for the **incompressible flow**.

* * *

Navier-Stokes Equations
-----------------------

Therefore, we have derived the Navier-Stokes Equations of an incompressible flow.

\[latex\] \\eqalign{ \\nabla \\cdot \\vec{V}=0 } \[/latex\] ,

\[latex\] \\eqalign{ \\frac{\\partial}{\\partial t}(\\rho\\vec{V}) +\\nabla\\cdot(\\rho\\vec{V} \\vec{V}) =\\rho\\vec{f} -\\nabla p +\\mu\\nabla^2\\vec{V} } \[/latex\] .

* * *

*   Reference:

1.  [Derivation of the Navier–Stokes equations](https://en.wikipedia.org/wiki/Derivation_of_the_Navier%E2%80%93Stokes_equations)
2.  [Fluid Dynamics: The Navier-Stokes Equations](http://andrew.gibiansky.com/downloads/pdf/Fluid%20Dynamics:%20The%20Navier-Stokes%20Equations.pdf)
3.  [Relations between stress and rate-of-strain tensors](http://web.mit.edu/1.63/www/Lec-notes/chap1_basics/1-6stress-strain.pdf)
4.  [The Reynolds Transport Theorem](https://www.me.psu.edu/cimbala/me320web_Spring_2015/pdf/Reynolds_transport_theorem.pdf)
5.  [Volume viscosity](https://en.wikipedia.org/wiki/Volume_viscosity)