---
title: Introduction of Moving Particle Semi-Implicit Method
tags:
  - Computational Fluid Dynamics (CFD)
id: '2011'
date: 2019-09-14 23:29:31
---

Governing Equations
-------------------

Governing equations are expressed by conservation of mass and momentum. The equations are:

\[latex\]\\eqalign{ \\frac{D\\rho}{Dt}+\\rho \\nabla \\cdot \\mathbf{u} =0 } \[/latex\]

and

\[latex\]\\eqalign{ \\frac{D \\mathbf{u} }{Dt}=-\\frac{1}{\\rho}\\nabla P +\\nu \\nabla^2 \\mathbf{u} +\\mathbf{f} } \[/latex\]

where \[latex\] \\rho\[/latex\] indicates density, \[latex\]P\[/latex\] is the pressure, \[latex\]\\mathbf{u}\[/latex\] the velocity and \[latex\]\\mathbf{f}\[/latex\] the external force.

It should be noted that the first equation is written in the form of compressible flow. In the MPS method, incompressibility is enforced by way of setting \[latex\]\\frac{ D \\rho}{D t}=0\[/latex\] at each particle at each calculation time step.

* * *

Particle Interaction Models
---------------------------

### Weighting functions

The particle interacts with its neighboring particles which are covered with a weight function \[latex\]w(\\bf{r})\[/latex\], where \[latex\]\\bf{r}\[/latex\] is the distance between two particles. There are many kinds of form for this weight function, we employed the following one:

\[latex\] w(\\bf{r}) = \\begin{cases} \\frac{r\_e}{r}-1 & ,0 \\leq r <r\_e \\\\  
0 & ,r>r \_e \\end{cases} \[/latex\]

For each particle, only a finite number of neighboring particles are related to the interactions.

### Particle number density \[latex\] \\langle n \\rangle\_i \[/latex\]

When a particle \[latex\]i\[/latex\] and its neighbors \[latex\]j\[/latex\] are located at \[latex\]\\bf{r\_i}\[/latex\] and \[latex\]\\bf{r\_j}\[/latex\], **particle number density** \[latex\] \\langle n \\rangle\_i \[/latex\] is defined as,

\[latex\]\\eqalign{ \\langle n \\rangle\_i = \\sum\_{i \\neq j} w\\left( | \\mathbf{r} \_j - \\mathbf{r}\_i | \\right )} \[/latex\].

The constant value of the particle number density is denoted by \[latex\]n^0\[/latex\].

### The number of particles in a unit volume \[latex\] \\langle N \\rangle\_i \[/latex\]

The number of particles in a unit volume, \[latex\] \\langle N \\rangle\_i \[/latex\], can be approximated by the particle number density:

\[latex\]\\eqalign{ \\langle N \\rangle\_i = \\frac{\\langle n \\rangle\_i}{\\int w( \\mathbf{r} )dv}} \[/latex\]

The denominator of this equation is the integral of the kernel in the whole region, excluding a central part occupied by particle \[latex\]i\[/latex\].

### Fluid density \[latex\] \\langle \\rho \\rangle\_i \[/latex\]

Assuming that the particles **have the same mass** \[latex\] m \[/latex\] , the fluid density, \[latex\] \\langle \\rho \\rangle\_i \[/latex\] is expressed as,

\[latex\] \\eqalign{ \\langle \\rho \\rangle\_i = m\\langle N \\rangle\_i = \\frac{m\\langle n \\rangle\_i}{\\int w( \\mathbf{r} )dv}} \[/latex\]

In the MPS method a fluid is represented by moving particles with constant mass. Thus, **the incompressibily of the fluid is guaranteed by keeping the particle number density** (\[latex\] \\langle n \\rangle\_i \[/latex\] ) **of the fluid constant.** The continuity equation is also satisfied automatically by keeping the total number of particles and the mass of individual particles constant.

* * *

Model of Mathematical Operator
------------------------------

Each mathematical operator acting on the arbitrary scalar \[latex\]\\phi\[/latex\] and vector \[latex\]\\mathbf{u}\[/latex\] at particle \[latex\]i\[/latex\] are defined as the particle interaction approximation as follows:

### Gradient operator

Represent by the weighted average of gradient vectors.

\[latex\] \\eqalign{  
\\langle \\nabla \\phi \\rangle\_i = \\frac{d}{n^0}\\sum\_{i \\neq j}  
\\frac{\\phi\_j-\\phi\_i}{| \\mathbf{r} \_j - \\mathbf{r}\_i |^2} \\left(\\mathbf{r} \_j - \\mathbf{r}\_i \\right)w\\left( | \\mathbf{r} \_j - \\mathbf{r}\_i | \\right )  
} \[/latex\]

where \[latex\] d \[/latex\] is the number of space dimensions, \[latex\] n^0 \[/latex\] is a particle number density ﬁxed for incompressibility.

### Laplacian operator

Part of a quantity contained by a particle \[latex\]i\[/latex\] is distributed to neighboring particles \[latex\]j\[/latex\] using the weight function.

\[latex\] \\eqalign{  
\\langle \\nabla^2 \\phi \\rangle\_i = \\frac{2d}{\\lambda n^0}\\sum\_{i \\neq j}  
\\left\[\\left(\\phi\_j-\\phi\_i\\right) w\\left( | \\mathbf{r} \_j - \\mathbf{r}\_i | \\right )\\right\]  
} \[/latex\]

where \[latex\] \\lambda \[/latex\] is

\[latex\]\\eqalign{ \\lambda = \\frac{\\int\_{V} w(r)r^2 dv}{\\int\_{V} w(r) dv} = \\frac{\\sum\_{i \\neq j} w \\left( | \\mathbf{r}\_j - \\mathbf{r}\_i | \\right) | \\mathbf{r}\_ j - \\mathbf{r}\_i |^2 }{ \\sum\_{i \\neq j} w \\left( | \\mathbf{r}\_j - \\mathbf{r}\_i | \\right) } }\[/latex\].

### Divergence operator

\[latex\] \\eqalign{  
\\langle \\nabla \\cdot \\mathbf{u} \\rangle\_i = \\frac{2d}{n^0}\\sum\_{i \\neq j}  
\\frac{ \\left( \\mathbf{u}\_j - \\mathbf{u}\_i \\right) \\cdot\\left(\\mathbf{r} \_j - \\mathbf{r}\_i \\right)}{| \\mathbf{r} \_j - \\mathbf{r}\_i |^2} w\\left( | \\mathbf{r} \_j - \\mathbf{r}\_i | \\right )  
} \[/latex\]

* * *

Step of Semi-implicit Algorithm
-------------------------------

*   **Initialize configuration of particles**:

\[latex\]\\mathbf{u}\_i^0, \\mathbf{r}\_i^0, P\_i^0 \[/latex\].

*   **Calculate the intermediate velocity \[latex\]\\mathbf{u}\_i^\*\[/latex\] from part of momentum equation.**

\[latex\] \\eqalign{ \\mathbf{u}\_i^\* = \\mathbf{u}\_i^n + \\Delta t & \\left( \\nu \\nabla^2 \\mathbf{u}\_i^n + \\mathbf{f} \\right) } \[/latex\].

*   **Calculate the intermediate** **coordinates of particles, \[latex\]\\mathbf{r}\_i^\*\[/latex\]**.

\[latex\] \\eqalign{ \\mathbf{r}\_i^\* = \\mathbf{r}\_i^n + \\Delta t & \\mathbf{u}\_i^\* } \[/latex\].

*   **Compute intermediate particle number density \[latex\]n^\*\[/latex\] by using intermediate particle locations**.

*   **Obtain pressure \[latex\]P\_i^{n+1}\[/latex\] by solving pressure Poisson equation.**

\[latex\] \\eqalign{ \\nabla^2 P\_i^{n+1} = -\\frac{\\rho}{\\Delta t^2}\\frac{n\_i^\*-n^0}{n^0} } \[/latex\].

*   **Finally, new velocity \[latex\] \\mathbf{u}\_i^{n+1} \[/latex\] and new coordinates of particles \[latex\] \\mathbf{r}\_i^{n+1} \[/latex\] are computed.**

\[latex\] \\eqalign{ \\mathbf{u}\_i^{n+1} = \\mathbf{u}\_i^\* - \\frac{ \\Delta t }{\\rho}\\nabla P\_i^{n+1} } \[/latex\].

\[latex\] \\eqalign{ \\mathbf{r}\_i^{n+1} = \\mathbf{r}\_i^n + \\Delta t & \\mathbf{u}\_i^{n+1} } \[/latex\].

* * *

Build System of Linear Equations
--------------------------------

*   **Linear Equations of intermediate velocity \[latex\]\\mathbf{u}\_i^\*\[/latex\]**.

\[latex\]\\eqalign{  
\\mathbf{u}\_i^\* = \\mathbf{u}\_i^n + \\Delta t & \\left( \\nu \\frac{2d}{\\lambda n^0}\\sum\_{i \\neq j} \\left\[\\left(\\mathbf{u}^n\_j-\\mathbf{u}^n\_i\\right) w\\left( | \\mathbf{r} \_j - \\mathbf{r}\_i | \\right )\\right\] + \\mathbf{f} \\right)  
}\[/latex\].

*   **Linear Equations of intermediate** **coordinates of particles, \[latex\]\\mathbf{r}\_i^\*\[/latex\]**.

\[latex\] \\eqalign{ \\mathbf{r}\_i^\* = \\mathbf{r}\_i^n + \\Delta t & \\mathbf{u}\_i^\* } \[/latex\].

*   **Linear Equations of pressure \[latex\]P\_i^{n+1}\[/latex\] from pressure Poisson equation.**

\[latex\] \\eqalign{  
\\frac{2d}{\\lambda n^0}\\sum\_{i \\neq j}  
\\left\[\\left(P\_j-P\_i\\right) w\\left( | \\mathbf{r} \_j - \\mathbf{r}\_i | \\right )\\right\]  
\= -\\frac{\\rho}{\\Delta t^2}\\frac{n\_i^\*-n^0}{n^0}  
} \[/latex\].

*   **Linear Equations of new velocity \[latex\] \\mathbf{u}\_i^{n+1} \[/latex\] and new coordinates of particles \[latex\] \\mathbf{r}\_i^{n+1} \[/latex\].**

\[latex\] \\eqalign{  
\\mathbf{u}\_i^{n+1} = \\mathbf{u}\_i^\* - \\frac{ \\Delta t }{\\rho}\\frac{d}{n^0}\\sum\_{i \\neq j}  
\\frac{(P\_i-P\_j)\\cdot\\left(\\mathbf{r} \_j - \\mathbf{r}\_i \\right)}{| \\mathbf{r} \_j - \\mathbf{r}\_i |^2} w\\left( | \\mathbf{r} \_j - \\mathbf{r}\_i | \\right )  
}\[/latex\],

\[latex\] \\eqalign{ \\mathbf{r}\_i^{n+1} = \\mathbf{r}\_i^n + \\Delta t & \\mathbf{u}\_i^{n+1} } \[/latex\].

* * *

*   Reference:

1.  [A stable moving-particle semi-implicit method for free surface flows](https://www.sciencedirect.com/science/article/pii/S0169598305001322)
2.  [Moving Particle Semi-Implicit Method](https://www.wire.tu-bs.de/OLDWEB/akeese/seminarWS01/talks/mps_paper.pdf)