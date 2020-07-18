---
title: Turbulence Modeling – Boussinesq Eddy Viscosity & Mixing Length Theory
tags:
  - My Turbulence Modeling Note
  - Turbulence Modeling
id: '1143'
date: 2018-06-24 19:04:38
---

Boussinesq Eddy-Viscosity
-------------------------

From the derivations in [previous article](https://bhlin.co.network/wp/2018/06/13/turbulence-modeling-reynolds-averaged-transport-equations/), the Reynolds-averaged approach to turbulence modeling requires that the Reynolds stresses be appropriately modeled. **Boussinesq's eddy-viscosity** concept, which assumes that, in analogy to the viscous stresses in laminar flows, **the turbulent stresses are proportional to the mean velocity gradient**.

\[latex\] \\eqalign{ \\left\\{ \\begin{aligned} &-\\mathbf{R}^{ij} = -\\frac{2}{3}g^{ij}k+2\\boldsymbol{\\nu\_t}\\overline{e}^{ij} &\\textrm{Turbulent}\\\\ &-\\boldsymbol{\\sigma}^{ij} = -pg^{ij}+2\\boldsymbol{\\nu}e^{ij} &\\textrm{Larminar}\\\\ \\end{aligned} \\right. } \[/latex\] Turbulent Stresses vs. Mean-Rate-of-Strains

where the turbulence kinetic energy, \[latex\]k\[/latex\], is defined as

\[latex\] \\eqalign{ k = \\frac{1}{2} \\overline{v^i v^j} } \[/latex\]

and \[latex\] \\boldsymbol{\\nu\_t}\[/latex\] is the eddy viscosity assumed as an isotropic scalar quantity — **which is not strictly true** — so that the term “approximation” is appropriate. Only a breifly derivation of relation between Reynolds stresses and eddy viscosity are written below. See [the article](https://wiki.math.ntnu.no/_media/ma8502/2014h/cds13workbook.pdf) for further detail.

\[latex\] \\eqalign{ -\\mathbf{R}^{ij}=-\\overline{v^iv^j} = -\\frac{2}{3}g^{ij}k+\\boldsymbol{\\nu\_t}(g^{in}V^j\_{,n}+g^{jn}V^i\_{,n}) =-\\frac{2}{3}g^{ij}k+2\\boldsymbol{\\nu\_t}\\overline{e}^{ij} } \[/latex\]

Unfortunately the value of \[latex\] \\boldsymbol{\\nu\_t}\[/latex\] is not known. The term \[latex\] \\boldsymbol{\\nu}\[/latex\] is a property of the fluid whereas \[latex\] \\boldsymbol{\\nu\_t}\[/latex\] is attributed to random fluctuations and is not a property of the fluid. However, it is necessary to find out empirical relations between \[latex\] \\boldsymbol{\\nu\_t}\[/latex\], and the mean velocity. The following section discusses relation between the aforesaid apparent or eddy viscosity and the mean velocity components

* * *

Mixing Length Theory
--------------------

![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/10.8.gif) Source : http://www.nptel.ac.in/courses/112104118/lecture-33/33-5\_shear\_stress.htm

In direct analogy to the molecular transport of momentum, Prandtl’s mixing length model (1925) assumes that turbulent eddies cling together and maintain their momentum for a distance, \[latex\] l\_{mix}\[/latex\], and are propelled by some turbulent velocity, \[latex\] v\_{mix}\[/latex\]. With these assumptions, the Reynolds stress terms are modeled by

\[latex\] \\eqalign{ \\tau\_t =-\\rho\\overline{uv}= \\rho v\_{mix}l\_{mix}\\frac{\\partial U}{\\partial y} } \[/latex\].

for a two-dimensional shear flow as is shown in figure above. This theory further postulates that the mixing velocity, \[latex\] v\_{mix}\[/latex\], is of the same order of magnitude as the (horizontal) fluctuating velocities of the eddies, which can be supported through experimental results for a wide range of turbulent flows. With this assumption, we have

\[latex\] \\eqalign{ v\_{mix}\\approx \\lvert u\\lvert\\approx \\lvert v\\lvert\\approx \\lvert w\\lvert\\approx l\_{mix}\\lvert\\frac{\\partial U}{\\partial y}\\lvert } \[/latex\].

or, in terms of the eddy viscosity for a shear flow

\[latex\] \\eqalign{ \\nu\_t =\\rho(l\_{mix})^2\\lvert\\frac{\\partial U}{\\partial y}\\lvert } \[/latex\].

This definition for the eddy viscosity can also be implied on dimensional grounds. With these definitions in mind, the objective of most algebraic models (zero-equation models) is to find some prescription for the turbulent mixing length, \[latex\] l\_{mix}\[/latex\], in order to provide closure.

* * *

*   Reference:

1.  [A note on the mixing length theory of turbulent flow](http://onlinelibrary.wiley.com/doi/10.1002/aic.690160532/pdf)
2.  [Ismail B. Celik, "Introductory Turbulence Modeling"](https://wiki.math.ntnu.no/_media/ma8502/2014h/cds13workbook.pdf)
3.  [Turbulence Modeling](http://www.mit.edu/~cuongng/Site/Publication_files/TurbulenceModeling_04NOV05.pdf)
4.  [Turbulence flow](http://www.nptel.ac.in/courses/112104118/lecture-33/33-5_shear_stress.htm)
5.  [Algebraic turbulence models](https://www.cfdsupport.com/OpenFOAM-Training-by-CFD-Support/node326.html)