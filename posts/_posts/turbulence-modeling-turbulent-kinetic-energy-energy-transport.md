---
title: Turbulence Modeling - Turbulent Kinetic Energy & Energy Transport
tags:
  - computational fluid dynamics
  - My Turbulence Modeling Note
  - Turbulence Modeling
id: '1116'
date: 2018-06-19 00:09:48
---

Turbulent Kinetic Energy and Turbulence Modeling
------------------------------------------------

As an alternative to the **algebraic or mixing length model**, one-equation models have been developed in an attempt to improve turbulent flow predictions by solving one additional transport equation. While several different turbulent scales have been used as the variable in the extra transport equation, the most popular method is to solve for the characteristic turbulent velocity scale proportional to the square root of the specific **kinetic energy of the turbulent fluctuations**. This quantity is usually just referred to as the **turbulence kinetic energy** and is denoted by \[latex\]k\[/latex\]. The Reynolds stresses are then related to this scale in a similar manner in which \[latex\]\\tau^{ij}\[/latex\] (reynolds stresses) was related to \[latex\]l\_{max}\[/latex\] (mixing length) in algebraic models. Since the modeled \[latex\]k\[/latex\] equation is generally the basis for all one and two equation models, the exact differential equation for the turbulence kinetic energy, and the physical interpretation of the terms in the turbulence kinetic energy equation, will be derived first. Then, with some understanding of the energy equations, the energy transportation in turbulence flow is discussed.

* * *

Turbulent Kinetic Energy Equation
---------------------------------

Turbulent kinetic energy can be quantified by the mean of the turbulence normal stresses:

\[latex\] \\eqalign{ k=\\frac{1}{2}\\overline{\\vec{v}\\cdot\\vec{v}}=\\frac{1}{2}\\overline{(v^i\\vec{a\_i})\\cdot (v^j\\vec{a\_j})}=\\frac{1}{2}g\_{ij}\\overline{v^iv^j} } \[/latex\]

Contractiing [Reynolds stress equations](https://bhlin.co.network/wp/2018/06/13/turbulence-modeling-reynolds-averaged-transport-equations/#Reynolds_Stresses_Transport_Equations) by turbulent kinetic energy \[latex\]k\[/latex\], this gives us **transport of turbulent kinetic energy**:

\[latex\] \\eqalign{ \\begin{aligned} \\frac{\\partial k}{\\partial t}& +V^mk\_{,m}+g\_{ij}\\overline{v^jv^m}V\_{,m}^i+\\frac{1}{2}(g\_{ij}\\overline{v^iv^jv^m})\_{,m}+(\\frac{\\overline{v^m p'}}{\\rho})\_{,m}\\\\ &-g\_{ij}\\overline{f^iv^j}-\\nu g^{mn}k\_{,mn}+\\nu g\_{ij}g^{mn}\\overline{v^i\_{,m}v^j\_{,n}}=0 \\end{aligned} } \[/latex\]

Rearrange the eqaution above, and we have

\[latex\] \\eqalign{ \\begin{aligned} \\frac{D k}{D t} &=\\frac{\\partial k}{\\partial t} +V^mk\_{,m}\\\\ & =-g\_{ij}\\overline{v^jv^m}V\_{,m}^i+\\left\[\\nu g^{mn}k\_{,n}-\\frac{\\overline{v^m p'}}{\\rho} -\\frac{1}{2}g\_{ij}\\overline{v^iv^jv^m}\\right\]\_{,m}+g\_{ij}\\overline{f^iv^j}-\\nu g\_{ij}g^{mn}\\overline{v^i\_{,m}v^j\_{,n}} \\end{aligned} } \[/latex\]

The meaning of each term in turbulent kinetic energy equation is list as following:

\[latex\] \\eqalign{ \\left\\{ \\begin{aligned} &\\frac{\\partial k}{\\partial t} +V^mk\_{,m}& \\textrm{convection}\\\\ &g\_{ij}\\overline{v^jv^m}V\_{,m}^i& \\textrm{Production}\\\\ &\\left\[\\nu g^{mn}k\_{,n}-\\frac{\\overline{v^m p'}}{\\rho} -\\frac{1}{2}g\_{ij}\\overline{v^iv^jv^m}\\right\]\_{,m}& \\textrm{Diffusion}\\\\ &g\_{ij}\\overline{f^iv^j}& \\textrm{Force field}\\\\ &\\nu g\_{ij}g^{mn}\\overline{v^i\_{,m}v^j\_{,n}}& \\textrm{Disspation}\\\\ \\end{aligned} \\right. } \[/latex\]

* * *

Energy Dissipation Equation
---------------------------

Rate of **turbulent kinetic energy dissipation** is defined as:

\[latex\] \\eqalign{ \\boldsymbol{\\varepsilon} = \\nu g\_{ij}g^{rs}\\overline{v^i\_{,r}v^j\_{,s}} } \[/latex\]

which is the last term we show in the turbulent kinetic energy equation above. The transport equation of \[latex\]\\boldsymbol{\\varepsilon}\[/latex\] can be derived from the contraction of [fluctuating momentum equations](https://bhlin.co.network/wp/2018/06/13/turbulence-modeling-reynolds-averaged-transport-equations/#Reynolds_Averaged_Navier-Stokes_Equations) \[latex\]m^i\[/latex\]. After some derivations, energy dissipation equation can be written as: ![Alt text](https://bhlin.co.network/wp/wp-content/uploads/2018/06/未命名.png) The meaning of each term in energy dissipation equation is list as following:

1.  Convective terms following the mean motion.
2.  Diffusion terms due to: (a) velocity fluctuations, (b) pressure fluctuations, (c) molecular actions.
3.  Production terms by mean flow gradient due to : (a) vortex stretching, (b) secondary generation.
4.  Generation due to “vortex stretching” by turbulence (no mean flow involved).
5.  Force field (e.g., buoyancy \[latex\]f^j\[/latex\] = \[latex\]\\beta g^j \\theta\[/latex\] ).
6.  Viscous destruction of \[latex\]\\boldsymbol{\\varepsilon}\[/latex\].

* * *

Energy Transport of turbulence flow
-----------------------------------

The energy transportation in turbulence flow is discussed in this part.

### Mean kinetic energy equation

We define the **mean kinetic energy** as

\[latex\] \\eqalign{ K=\\frac{1}{2}g\_{ij}V^iV^j } \[/latex\].

Multiply [**mean momentum eqaution**](https://bhlin.co.network/wp/2018/06/13/turbulence-modeling-reynolds-averaged-transport-equations/#Reynolds_Averaged_Navier-Stokes_Equations) by \[latex\] g\_{ij}V^j \[/latex\], we have \[latex\] g\_{ij}V^jM^i \[/latex\]. The mean kinetic energy equation can be derived as:

\[latex\] \\eqalign{ \\begin{aligned} \\frac{D K}{D t} &=\\frac{\\partial K}{\\partial t} +V^mK\_{,m}\\\\ &= g\_{ij}F^iV^j+\\left\[\\nu g^{mn}K\_{,n}-\\frac{V^m p}{\\rho} -g\_{ij}\\overline{v^iv^m}V^j\\right\]\_{,m}+g\_{ij}\\overline{v^iv^m}V\_{,m}^j-\\nu g\_{ij}g^{mn}V^i\_{,m}V^j\_{,n} \\end{aligned} } \[/latex\].

### Thermal Energy Equation

Thermal energy and temperature also can be expressed as the sum of **mean** and **fluctuating** parts:

\[latex\] \\eqalign{ \\left\\{ \\begin{aligned} &e^\*= E+e ,& \\textrm{thermal energy}\\\\ &T\*= T + \\theta ,& \\textrm{ temperature}\\\\ \\end{aligned} \\right. } \[/latex\].

The thermal energy equation can be written as:

\[latex\] \\eqalign{ \\frac{D e^\*}{D t} =\\frac{1}{\\rho}(\\kappa g^{ij}T^\*\_{,n})\_{,m}+\\frac{1}{\\rho}\\boldsymbol{\\Phi}+\\boldsymbol{Q}; \\quad \\boldsymbol{\\Phi}=\\mu(v^i\_{,j}v^j\_{,i}+g\_{ij}g^{mn}v^i\_{,m}v^j\_{,n}) } \[/latex\].

Substituting the **mean** and **fluctuating** parts of the field variables into equation above, we can obtain:

\[latex\] \\eqalign{ \\begin{aligned} \\frac{D E}{D t} &=\\frac{\\partial E}{\\partial t} +V^mE\_{,m}\\\\ &=\\boldsymbol{Q}+\\frac{1}{\\rho}(\\kappa g^{mn}T\_{,n})\_{,m}-(\\overline{v^m e})\_{,m}+\\nu\\left(V^mV^n+\\overline{v^m v^n}\\right)\_{,mn}+\\nu g\_{ij}g^{mn}\\left(V^i\_{,m}V^j\_{,n}+\\overline{v^i\_{,m} v^j\_{,n}}\\right) \\end{aligned} } \[/latex\].

where the physical meaning of each term can be expressed as:

\[latex\] \\eqalign{ \\left\\{ \\begin{aligned} &(\\overline{v^m e})\_{,m}& \\textrm{turbulent heat fluxes}\\\\ & \\nu\\left(V^mV^n+\\overline{v^m v^n}\\right)\_{,mn}+\\nu g\_{ij}g^{mn}\\left(V^i\_{,m}V^j\_{,n}+\\overline{v^i\_{,m} v^j\_{,n}}\\right)& \\textrm{dissipation function} \\end{aligned} \\right. } \[/latex\].

### Total Energy Transportation

The total energy in the turbulence flow can be defined as \[latex\] E\_{total} = K + k + E\[/latex\]. With the energy equations we derive above, we can obtain the equation for total energy.

\[latex\] \\eqalign{ \\frac{D}{Dt}(K+k+E)=\\left\\{g\_{,ij}(F^iV^j+\\overline{f^iv^j})+Q\\right\\}+\\left\\{\\textrm{diffusion}\\right\\}\_{,m} } \[/latex\]

Then, we list all energy equations and gives a summerize. ![Alt text](https://bhlin.co.network/wp/wp-content/uploads/2018/06/未命名-1.png) We conclude that,

*   Conservation of total energy in the absence of external forces and heat generation (energy redistribution by diffusion) .
*   Turbulence extracts energy from mean flow (turbulent production, large scale) and dissipates into heat (thermal energy dissipation, small scale).

* * *

*   Reference:

1.  [Ismail B. Celik, "Introductory Turbulence Modeling"](https://wiki.math.ntnu.no/_media/ma8502/2014h/cds13workbook.pdf)
2.  [Which Turbulence Model Should I Choose for My CFD Application?](https://www.comsol.com/blogs/which-turbulence-model-should-choose-cfd-application/)
3.  [Reynolds-averaged Navier–Stokes equations](https://en.wikipedia.org/wiki/Reynolds-averaged_Navier%E2%80%93Stokes_equations)
4.  [Introduction to turbulence/Reynolds averaged equations](https://www.cfd-online.com/Wiki/Introduction_to_turbulence/Reynolds_averaged_equations)
5.  [Turbulence](https://cefrc.princeton.edu/sites/cefrc/files/Files/2014%20Lecture%20Notes/Pitsch/Lecture7_Turbulence_2014.pdf)
6.  [Turbulence Modeling](http://www.mit.edu/~cuongng/Site/Publication_files/TurbulenceModeling_04NOV05.pdf)
7.  [Advanced Computation Methods for Fluid Flow - 2018](https://bhlin.co.network/wp/category/lecture-notes/advanced-computation-methods-for-fluid-flow-2018/)
8.  [CCFD 5050: Turbulent Flow](https://homepages.see.leeds.ac.uk/~amt6xw/Distance%20Learning/CFD5050TURB/cfd5050_TURB.html)
9.  [Simulation of Turbulent Flows](https://web.stanford.edu/class/me469b/handouts/turbulence.pdf)
10.  [Turbulence kinetic energy - TKE](http://mafija.fmf.uni-lj.si/seminar/files/2011_2012/MaticSavli_2.pdf)