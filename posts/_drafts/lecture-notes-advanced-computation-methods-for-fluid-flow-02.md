---
title: '[Lecture Notes] Advanced Computation Methods for Fluid Flow – 02'
tags:
  - Advanced Computation Methods for Fluid Flow - 2018
  - computational fluid dynamics
  - numerical method
id: '282'
---

> _14/03/2018, Chapter1 - Introduction and General Equations_

* * *

Fundamental Laws in Fluid Mechanics
-----------------------------------

First, we list some fundamental laws and their corresponding equations which are often considered in fluid mechanics.

*   **Conservation of geometry of motion and deformation of matter** - translation, rotation, linear and angular deformations (fluid kinematics).
*   **Conservation of mass** - continuity equation.
*   **Conservation of momentum** - newton's second law.
*   **Conservation of angular momentum**
*   **Conservation of energy** - second law of thermodynamics.
*   Equation of sate, stress/rate of strain relations, Fourier law, and other constitutive equation.

The equations for conservation of mass, momentum and energy in Eulerian description will be derived in this article.

* * *

Reynolds Transport Theorem
--------------------------

Two ways are generally used in describing fluid motion for mathematical analysis, the Lagrangian description and the Eulerian description.

*   **Lagrangian description** (Particle approach) The Lagrangian method describes the behavior of the individual fluid during its course of motion through space. We focus on the fluid in **material volume system** where the fluid will move, distort, and change size and shape, but always consists of the same fluid particles.
*   **Eulerian description** (Field approach) In the Eulerian method, the individual fluid particles are not identified. Instead, a fixed position in space is chosen, and the velocity of particles at this position as a function of time is sought. We focus attention on what happens at a **fixed point (or volume)** as different fluid particles goes by.

**Reynolds Transport Theorem** provide the link between these two descriptions. The following equation shows how the convertion is done between Lagrangian to Eulerian description.

\[latex\]\\eqalign{\\frac{D}{Dt}\\int\\limits\_{MV(t)}F(\\vec{\\mathrm{r}},t)\\mathrm{d}\\Omega=\\frac{d}{dt}\\int\\limits\_{CV(t)}F(\\vec{\\mathrm{r}},t) \\ \\mathrm{d}\\Omega + \\oint\\limits\_{CS(t)}F(\\vec{\\mathrm{r}},t)\\vec{V}\\cdot \\vec{n}\\ \\mathrm{d}S}\[/latex\]

Usually, we use **divergence theorem** ( \[latex\]\\int\\vec{\\mathrm{A}} \\cdot \\vec{n} \\ \\mathrm{d}S=\\int\\nabla \\cdot \\vec{\\mathrm{A}} \\ \\mathrm{d}\\Omega\[/latex\] ) to convert surface integrals in above equation into volume integrals. Then, this gives us a conversion formulation.

\[latex\]\\eqalign{ \\frac{D}{Dt}\\int\\limits\_{MV}F\\ \\mathrm{d}\\Omega=\\frac{d}{dt}\\int\\limits\_{CV} F\\ \\mathrm{d}\\Omega + \\int\\limits\_{CV}\\nabla\\cdot (F\\vec{V})\\ \\mathrm{d}\\Omega\\\\ \\qquad\\qquad=\\int\\limits\_{CV}\\left\[ \\frac{\\partial F}{\\partial t} + \\vec{V}\\cdot \\nabla F+F \\nabla \\cdot \\vec{V} \\right\]{d}\\Omega\\\\ \\quad=\\int\\limits\_{CV}\\frac{DF}{Dt} \\ \\mathrm{d}\\Omega + \\int\\limits\_{CV}F\\nabla\\cdot\\vec{V}\\ \\mathrm{d}\\Omega }\[/latex\]

Let \[latex\] F = \\rho \\ \\phi \[/latex\], then we have,

\[latex\]\\eqalign{ \\frac{D}{Dt}\\int\\limits\_{MV}\\rho \\ \\phi\\ \\mathrm{d}\\Omega=\\int\\limits\_{CV}\\frac{D(\\rho \\ \\phi)}{Dt} \\ \\mathrm{d}\\Omega + \\int\\limits\_{CV}\\rho \\ \\phi\\nabla\\cdot\\vec{V}\\ \\mathrm{d}\\Omega }\[/latex\]

* * *

Conservation of Mass
--------------------

In lagrangian description, the equation for conservation of mass is written as,

\[latex\]\\eqalign{ \\frac{Dm}{Dt} =\\frac{D}{Dt}\\int\\limits\_{MV}\\rho\\ \\mathrm{d}\\Omega=0 \\ . }\[/latex\]

Which indicates that the \[latex\] \\phi \[/latex\] equals to 1 in conversion formulation. Hence, the conversion formulation becomes,

\[latex\]\\eqalign{ \\frac{D}{Dt}\\int\\limits\_{MV}\\rho \\ \\ \\mathrm{d}\\Omega=\\int\\limits\_{CV}\\frac{D\\rho \\ }{Dt} \\ \\mathrm{d}\\Omega + \\int\\limits\_{CV}\\rho \\ \\nabla\\cdot\\vec{V}\\ \\mathrm{d}\\Omega }\[/latex\]

Consider the incompressible flow in our applications, the fluid flow can be described in lagrangian and eulerian views are:

*   Lagrangian : \[latex\]\\frac{D\\rho}{Dt}=0\[/latex\].
*   Eulerian : \[latex\]\\frac{\\partial \\rho}{\\partial t}+\\vec{V}\\cdot\\nabla\\rho=0\[/latex\].

Take the equation of Eulerian view into conversion formulation above, it gives us,

\[latex\]\\eqalign{ \\nabla\\cdot\\vec{V}=0 }\[/latex\]

Here we obtain the **continuity equation**.

* * *

Conservation of Momentum
------------------------

Momentum equation is obtained when the conservation relation is applied to momentum. Base on the **Newton's Second Law** (\[latex\]F = ma \[/latex\]), the momentum equation in lagarangian description can be written as

\[latex\]\\eqalign{ \\frac{D}{Dt}\\int\\limits\_{MV}\\vec{V}\\rho \\ d\\Omega =\\int\\limits\_{MV}\\vec{f}\\rho\\ \\mathrm{d}\\Omega+ \\int\\limits\_{MS}\\vec{t} \\vec{n} \\ \\mathrm{d}S }\[/latex\]

where \[latex\]\\vec{t} = \\overline{\\overline{T}}\\cdot\\vec{n}\[/latex\] is surface force and \[latex\]\\overline{\\overline{T}} = T^{ij}\\vec{a\_i}\\vec{a\_j}\[/latex\] is stress tensor. The term in LHS indicates **rate of change of momentum in MV**, and the first and second term in RHS represent **body force** and **surface force**. By using Reynolds Transport Theorem, the LHS of the above equation can be transformed into Eulerian description.

\[latex\]\\eqalign{ \\frac{D}{Dt}\\int\\limits\_{MV}\\vec{V}\\rho \\ d\\Omega =\\frac{d}{dt}\\int\\limits\_{CV}\\vec{V}\\rho\\ \\mathrm{d}\\Omega+ \\int\\limits\_{CS}\\vec{V}\\rho\\vec{V}\\cdot \\vec{n} \\ \\mathrm{d}S }\[/latex\]

Then, the momentum equation in eulerian description can be obtained.

\[latex\]\\eqalign{ \\frac{d}{dt}\\int\\limits\_{CV}\\vec{V}\\rho\\ \\mathrm{d}\\Omega+ \\int\\limits\_{CS}\\vec{V}\\rho\\vec{V}\\cdot \\vec{n} \\ \\mathrm{d}S=\\int\\limits\_{CV}\\rho \\vec{f} \\ \\mathrm{d}\\Omega +\\int\\limits\_{CS}\\overline{\\overline{T}}\\cdot \\vec{n} \\ \\mathrm{d}S }\[/latex\]

Integrate every term in rbitrary but fixed control volume (by divergence theorem)

\[latex\]\\eqalign{ \\int\\limits\_{CV}\\left\[\\frac{\\partial}{\\partial t}(\\rho\\vec{V}+\\nabla\\cdot(\\rho\\vec{V}\\vec{V})-\\rho\\vec{f}-\\nabla\\cdot\\overline{\\overline{T}} \\right\] \\mathrm{d} \\Omega=0 }\[/latex\].

And the differential form is,

\[latex\]\\eqalign{ \\frac{\\partial}{\\partial t}(\\rho\\vec{V})+\\nabla\\cdot(\\rho\\vec{V}\\vec{V})=\\rho\\vec{f}+\\nabla\\cdot\\overline{\\overline{T}} }\[/latex\],

or,

\[latex\]\\eqalign{ \\rho\\frac{D\\vec{V}}{Dt}=\\rho\\vec{f}+\\nabla\\cdot\\overline{\\overline{T}} }.\[/latex\]

Assume the fluid to be newtionian fluid, the stress is linearly propotional to rate of strain. We can derivative **Navier-Stokes Equations** with compressible flow and incompressible flow.

*   For compressible flow:
    
    \[latex\]\\eqalign{ \\rho\\frac{D\\vec{V}}{Dt}=\\rho\\vec{f}-\\nabla p+\\frac{1}{3}\\mu\\nabla(\\nabla\\cdot\\vec{V})+\\mu\\nabla^2\\vec{V} }.\[/latex\]
    
*   For incompressible flow:
    
    \[latex\]\\eqalign{ \\rho\\frac{D\\vec{V}}{Dt}=\\rho\\vec{f}-\\nabla p+\\mu\\nabla^2\\vec{V} }.\[/latex\]
    

* * *

Conservation of Energy
----------------------

By **First Law of Thermodynamics**, the conservation of energy in Lagragian description can be expressed as

\[latex\]\\eqalign{ \\frac{DE}{Dt}=Q-W }.\[/latex\]

where \[latex\]\\frac{DE}{Dt}\[/latex\] is **rate of change of energy in MV**, \[latex\]Q\[/latex\] is **heat added to the system**, and \[latex\]W\[/latex\] is the **work done by the system**. The LHS term can be represented by internal and kinetic energy. The equation becomes

\[latex\]\\eqalign{ \\frac{DE}{Dt}=\\frac{D}{Dt}\\int\\limits\_{MV}\\rho(e+\\frac{1}{2}\\vec{V}\\cdot\\vec{V})\\mathrm{d} \\Omega \\qquad\\qquad\\qquad\\\\= -\\int\\limits\_{MV}\\vec{q}\\cdot\\vec{n} \\ \\mathrm{d} S +\\int\\limits\_{MV}Q\\ \\mathrm{d} \\Omega +\\int\\limits\_{MV}\\vec{V}\\cdot\\rho\\vec{f} \\ \\mathrm{d} \\Omega +\\int\\limits\_{MS}\\vec{t}(\\vec{n})\\cdot\\vec{V} \\ \\mathrm{d} S ,}\[/latex\]

where \[latex\]e\[/latex\] is the internal energy and the four terms in the RHS are **consition heat flux**, **heat generation**, **work done by body force**, **work done by surface force**. By using Reynolds Transport Theorem, \[latex\]\\frac{DE}{Dt}\[/latex\] can be transformed into Eulerian description.

\[latex\]\\eqalign{ \\frac{DE}{Dt}=\\int\\limits\_{CV}\\rho\\frac{D}{Dt}(e+\\frac{1}{2}\\vec{V}\\cdot\\vec{V})\\mathrm{d} \\Omega }\[/latex\]

and through some derivation

\[latex\]\\eqalign{ RHS = -\\int\\limits\_{MV}\\vec{q}\\cdot\\vec{n} \\ \\mathrm{d} S +\\int\\limits\_{MV}Q\\ \\mathrm{d} \\Omega +\\int\\limits\_{MV}\\vec{V}\\cdot\\rho\\vec{f} \\ \\mathrm{d} \\Omega +\\int\\limits\_{MS}\\vec{t}(\\vec{n})\\cdot\\vec{V} \\ \\mathrm{d} S \\\\= -\\int\\limits\_{CV}\\nabla\\cdot\\vec{q} \\ \\mathrm{d} \\Omega +\\int\\limits\_{CV}Q\\ \\mathrm{d} \\Omega +\\int\\limits\_{CV}\\rho\\vec{f}\\cdot\\vec{V} \\ \\mathrm{d} \\Omega +\\int\\limits\_{CV}\\nabla\\cdot(\\overline{\\overline{T}}\\cdot\\vec{V}) \\mathrm{d} \\Omega .}\[/latex\]

Now, the differential form of energy equation is

\[latex\]\\eqalign{ \\rho\\frac{D}{Dt}(e+\\frac{1}{2}\\vec{V}\\cdot\\vec{V})=\\nabla\\cdot(\\overline{\\overline{T}}\\cdot\\vec{V})+\\rho\\vec{f}\\cdot\\vec{V}-\\nabla\\cdot\\vec{q}+Q .}\[/latex\]

Consider the mechanical energy equation (multiply the momentum equation by \[latex\]\\vec{V}\[/latex\]), the above equation become

\[latex\]\\eqalign{ \\rho\\frac{De}{Dt}=(\\overline{\\overline{T}}\\cdot\\nabla)\\cdot\\vec{V}-\\nabla\\cdot\\vec{q}+Q .}\[/latex\]

Further consider the **Fourier's law for conduction**( \[latex\]\\vec{q} =-\\kappa\\nabla T\[/latex\]), the energy equation become

\[latex\]\\eqalign{ \\rho\\frac{De}{Dt}=-p\\nabla\\cdot\\vec{V}+\\Phi+ \\nabla \\cdot(\\kappa \\nabla T)+Q ,}\[/latex\]

where \[latex\]\\Phi =\\lambda(\\nabla\\cdot\\vec{V})^2+2\\mu \\overline{\\overline{D}}:\\overline{\\overline{D}}\[/latex\]. The four terms in the RHS are **compression work**, **dissipation**, **conduction**, and **heat generation**, respectively. Finally, assume incrompressible flow and constant \[latex\]\\kappa\[/latex\], then we obtain

\[latex\]\\eqalign{ \\rho C\_v\\frac{DT}{Dt}=2\\mu \\overline{\\overline{D}}:\\overline{\\overline{D}}+ \\kappa \\nabla^2 T+Q .}\[/latex\]

* * *

Generic Conservation Equation
-----------------------------

*   **Integral form**:
    
    \[latex\]\\eqalign{ \\frac{\\partial}{\\partial t}\\int\\limits\_{CV}\\rho\\phi\\ \\mathrm{d}\\Omega+ \\int\\limits\_{CS}\\rho\\phi\\vec{V}\\cdot \\vec{n} \\ \\mathrm{d}S=\\int\\limits\_{CS}\\Gamma \\nabla \\phi\\cdot\\vec{n} \\ \\mathrm{d}S +\\int\\limits\_{CV}q\_\\phi\\ \\mathrm{d}\\Omega .}\[/latex\]
    
*   **Vector form**:
    
    \[latex\]\\eqalign{ \\frac{\\partial}{\\partial t}(\\rho\\phi)+ \\nabla\\cdot(\\rho\\phi\\vec{V}) =\\nabla\\cdot(\\Gamma \\nabla \\phi) +q\_\\phi .}\[/latex\]
    

\[latex\]\\Gamma\[/latex\] : diffusivity for \[latex\]\\phi\[/latex\]; \[latex\]q\_\\phi\[/latex\] : source/sink of \[latex\]\\phi\[/latex\].