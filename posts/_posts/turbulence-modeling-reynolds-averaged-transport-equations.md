---
title: Turbulence Modeling - Reynolds Averaged  Transport Equations
tags:
  - computational fluid dynamics
  - My Turbulence Modeling Note
  - Turbulence Modeling
id: '1016'
date: 2018-06-13 10:40:43
---

Reynolds Averaged Navier-Stokes Equations
-----------------------------------------

Considering the fluid flow over a flat plate, as shown in the figure below. The uniform velocity profile hits the leading edge of the flat plate, and a laminar boundary layer begins to develop. The flow in this region is very predictable. After some distance, small chaotic oscillations begin to develop in the boundary layer and the flow begins to transition to turbulence, eventually becoming fully turbulent.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/圖片1-1.png) Source : https://www.comsol.com/blogs/which-turbulence-model-should-choose-cfd-application/

In this flow regime, we can use a Reynolds-averaged Navier-Stokes (RANS) formulation, which is based on the observation that the flow field (\[latex\]v^i\_\*\[/latex\]) over time contains small, local oscillations (\[latex\]v^i\[/latex\]) and can be treated in a time-averaged sense (\[latex\]V^i\[/latex\]).

*   **Reynolds-averaging (ensemble average)** Hence, the field variables must be expressed as the sum of **mean** and **fluctuating** parts as `Instantaneous = Mean (ensemble) + fluctuation`
    
    \[latex\]\\eqalign{ \\left\\{ \\begin{aligned} &v^i\_\*= V^i+v^i ,& \\textrm{velocity}\\\\ &p\_\*= p+p' ,& \\textrm{pressure}\\\\ &\\rho\_\*= \\rho+\\rho' ,& \\textrm{density (compressible flow)}\\\\ &f^i\_\*= F^i+f^i ,& \\textrm{force field}\\\\ &T\_\*= T+\\theta , & \\textrm{temperature (heat transfer)}\\\\ \\end{aligned} \\right. }\[/latex\]
    
    where the mean and fluctuating parts satisfy
    
    \[latex\]\\eqalign{ &\\overline{v^i\_\*}=V^i\\ ,\\qquad \\overline{v^i}=0\\ \\\\ &\\overline{p\_\*}=P\\ ,\\qquad \\overline{p}=0\\ \\\\ &\\qquad\\qquad\\vdots }\[/latex\]
    
    The symbol with an overbar indicates the averaging.
    
*   **Averaging of Continuity Equation** For incompressible flow, the continuity equation in tensor notation can be written as
    
    \[latex\]\\eqalign{ v^i\_{\*,i}=0 }\[/latex\]
    
    We take time average on continuity equation and insert the relation derived above.
    
    \[latex\]\\eqalign{ \\overline{v^i\_{\*,i}}=\\overline{V^i\_{,i}+v^i\_{,i}}=\\overline{V^i\_{,i}}+\\overline{v^i\_{,i}}=V^i\_{,i}=0 }\[/latex\]
    
    Both the mean and fluctuating velocities satisfy the continuity equation. And the Continuity Equation of mean part velovity is
    
    \[latex\]\\eqalign{ V^i\_{,i}=0 }\[/latex\]
    
*   **Averaging of Momentum Equations** For incompressible flow, the momentum equation(instantaneous) in tensor notation can be expressed as
    
    \[latex\]\\eqalign{ \\frac{\\partial v^i\_{\*}}{\\partial t} + v^j\_{\*} v^i\_{\*,j}=f^i\_\*-\\frac{1}{\\rho}g^{ij}p\_{\*,j}+\\nu g^{mn}v^i\_{\*,mn} }\[/latex\]
    
    Again, we insert the relation derived above.
    
    \[latex\]\\eqalign{ \\frac{\\partial}{\\partial t}(V^i+v^i) + (V^j+v^j) (V^i+v^i)\_{,j}=(F^i+f^i)-\\frac{1}{\\rho}g^{ij}(p+p')\_{,j}+\\nu g^{mn}(V^i+v^i)\_{,mn} }\[/latex\]
    
    Take time average on this eqaution, and we obtain the **mean** momentum eqaution.
    
    \[latex\]\\eqalign{ \\frac{\\partial V^i}{\\partial t} +V^j V^i\_{,j}+\\overline{v^iv^i\_{,j}}=F^i-\\frac{1}{\\rho}g^{ij}p\_{,j}+\\nu g^{mn}V^i\_{,mn} }\[/latex\]
    
    where the \[latex\]\\overline{v^iv^i\_{,j}}\[/latex\] term is kown as the **Reynolds stresses** term. Reynolds stresses term **resulted from convective term**, not the viscous stress terms! On the other hand, the **flutuating** momentum eqaution can be derived by `Fluctuating = Instantaneous-Mean` and written as
    
    \[latex\]\\eqalign{ \\frac{\\partial v^i}{\\partial t} +V^j v^i\_{,j}+v^j V^i\_{,j}-\\overline{v^iv^i\_{,j}}=f^i-\\frac{1}{\\rho}g^{ij}p'\_{,j}+\\nu g^{mn}v^i\_{,mn} }\[/latex\]
    
    where
    
    \[latex\]\\eqalign{ v^j\_{,j}=0 \\qquad \\Rightarrow \\qquad \\overline{v^iv^i\_{,j}}=\\overline{(v^iv^i)\_{,j}} }\[/latex\]
    

* * *

Reynolds Stresses Transport Equations
-------------------------------------

In the Reynolds averaged momentum equation, **Reynolds stresses** have been expressed as

\[latex\]\\eqalign{ \\tau^{ij}= \\overline{v^iv^i} }\[/latex\]

To find an equation for the Reynolds stresses, we construct a equation \[latex\]v^i m^j+v^j m^i\[/latex\]. \[latex\]m^i\[/latex\] is the instantaneous momentum fluctuation equation (see [here](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.452.9762&rep=rep1&type=pdf) for further detail). Derive it, and we have

\[latex\]\\eqalign{ \\begin{aligned} &\\frac{\\partial}{\\partial t}(\\overline{ v^i v^j}) +V^m (\\overline{ v^i v^j}) \_{,m}+(\\overline{ v^i v^m}V^j\_{,m}+\\overline{ v^j v^m}V^i\_{,m})+(\\overline{ v^i v^j v^m})\_{,m} \\\\ &-(\\overline{v^if^j+v^jf^i})+( g^{im}\\frac{\\overline{v^jp'}}{\\rho}+g^{jm}\\frac{\\overline{v^ip'}}{\\rho})-\\overline{\\frac{p'}{\\rho}(g^{im}v^j\_{,m}+g^{jm}v^i\_{,m})} \\\\ &-\\nu g^{mn}(\\overline{ v^i v^j})\_{,mn}+2\\nu g^{mn}(\\overline{ v^i\_{,m} v^j\_{,n}})=0 \\end{aligned} }\[/latex\].

Simplify the equation with some symbols

\[latex\]\\eqalign{ \\frac{\\partial \\bf{R}^{ij}}{\\partial t}+\\bf{C}^{ij}=\\bf{P}^{ij}+\\bf{F}^{ij}+\\bf{D\_u}^{ij}+\\bf{D\_p}^{ij}+\\bf{D\_v}^{ij}++\\bf{\\Phi}^{ij}-\\boldsymbol{\\epsilon}^{ij} }\[/latex\].

This equation provide insight into the nature of the turbulent stresses. The meaning of each term is list as following.

\[latex\]\\eqalign{ \\left\\{ \\begin{aligned} &\\mathbf{R}^{ij}=\\overline{v^i v^j} ,& \\textrm{Reynolds stresses}\\\\ &\\mathbf{C}^{ij}=V^m\\mathbf{R}^{ij}\_m ,& \\textrm{Convection}\\\\ &\\mathbf{P}^{ij}=-(\\mathbf{R}^{im}V^j\_{,m}+\\mathbf{R}^{jm}V^i\_{,m})\\mathbf{R}^{ij}\_m ,& \\textrm{Production}\\\\ &\\mathbf{F}^{ij}=\\overline{f^i v^j}+\\overline{f^j v^i} ,& \\textrm{Force field}\\\\ &\\mathbf{D}^{ij}\_u=-(\\overline{v^i v^j v^m})\_{,m} ,& \\textrm{Diffusion by velocity fluctuation}\\\\ &\\mathbf{D}^{ij}\_p=-g^{im}\\frac{\\overline{v^jp'}}{\\rho}-g^{jm}\\frac{\\overline{v^ip'}}{\\rho} ,& \\textrm{Diffusion by Pressure fluctuation}\\\\ &\\mathbf{D}^{ij}\_v=\\nu g^{mn}(\\overline{ v^i v^j})\_{,mn} ,& \\textrm{Viscous Diffusion}\\\\ &\\mathbf{\\Phi}^{ij}=\\overline{\\frac{p'}{\\rho}(g^{im}v^j\_{,m}+g^{jm}v^i\_{,m})} ,& \\textrm{Pressure-strain}\\\\ &\\boldsymbol{\\epsilon}^{ij}=2\\nu g^{mn}(\\overline{ v^i\_{,m} v^j\_{,n}}) ,& \\textrm{Dissipation}\\\\ \\end{aligned} \\right. }\[/latex\].

With the derivation of the Reynolds stress equation, the influence on the stress term can be identified, but with the derivation new terms (higher order correlations) are generated which of themselves are unkown. By understanding how the turbulence behaves can one hope to guess an appropriate set of constitutive equations, the engineer must find some way to close the equations before they can be used. Finding closure problem for calculating these extra terms is the basis of turbulence modeling.

* * *

*   Reference:

1.  [Ismail B. Celik, "Introductory Turbulence Modeling"](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynb)
2.  [Which Turbulence Model Should I Choose for My CFD Application?](https://www.comsol.com/blogs/which-turbulence-model-should-choose-cfd-application/)
3.  [Reynolds-averaged Navier–Stokes equations](https://en.wikipedia.org/wiki/Reynolds-averaged_Navier%E2%80%93Stokes_equations)
4.  [Introduction to turbulence/Reynolds averaged equations](https://www.cfd-online.com/Wiki/Introduction_to_turbulence/Reynolds_averaged_equations)
5.  [Turbulence](https://cefrc.princeton.edu/sites/cefrc/files/Files/2014%20Lecture%20Notes/Pitsch/Lecture7_Turbulence_2014.pdf)
6.  [Turbulence Modeling](http://www.mit.edu/~cuongng/Site/Publication_files/TurbulenceModeling_04NOV05.pdf)
7.  [Advanced Computation Methods for Fluid Flow - 2018](https://bhlin.co.network/wp/category/lecture-notes/advanced-computation-methods-for-fluid-flow-2018/)