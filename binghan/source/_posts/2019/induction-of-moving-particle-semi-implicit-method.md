---
title: Introduction of Moving Particle Semi-Implicit Method
tags:
  - Computational Fluid Dynamics (CFD)
id: '2011'
date: 2019-09-14 23:29:31
mathjax: true
---

Governing Equations
-------------------

Governing equations are expressed by conservation of mass and momentum. The equations are:

$$
\eqalign{ \frac{D\rho}{Dt}+\rho \nabla \cdot \mathbf{u} =0 }
$$

and

$$
\eqalign{ \frac{D \mathbf{u} }{Dt}=-\frac{1}{\rho}\nabla P +\nu \nabla^2 \mathbf{u} +\mathbf{f} }
$$

where $\rho$ indicates density, $P$ is the pressure, $\mathbf{u}$ the velocity and $\mathbf{f}$ the external force. It should be noted that the first equation is written in the form of compressible flow. In the MPS method, **incompressibility is enforced by way of setting $\frac{ D \rho}{D t}=0$ at each particle at each calculation time step**.

<!-- more -->


* * *

Particle Interaction Models
---------------------------

### Weighting functions

The particle interacts with its neighboring particles which are covered with a weight function $w(\mathbf{r})$, where $\mathbf{r}$ is the distance between two particles. There are many kinds of form for this weight function, we employed the following one:

$$
\eqalign{
  w(\mathbf{r}) = \begin{cases} 
  \frac{r_e}{r}-1 & ,0 \leq r <r_e \\  
  0 & ,r>r_e \end{cases}
}
$$

For each particle, only a finite number of neighboring particles are related to the interactions.

### Particle number density $\langle n \rangle_i$

When a particle $i$ and its neighbors $j$ are located at $\mathbf{r_i}$ and $\mathbf{r_j}$, **particle number density** $\langle n \rangle_i$ is defined as,

$$
\eqalign{ 
  \langle n \rangle_i = \sum_{i \neq j} w\left( | \mathbf{r} _j - \mathbf{r}_i | \right )
}
$$

The constant value of the particle number density is denoted by $n^0$.

### The number of particles in a unit volume $\langle N \rangle_i$

The number of particles in a unit volume, $\langle N \rangle_i$, can be approximated by the particle number density:

$$
\eqalign{ 
\langle N \rangle_i = \frac{\langle n \rangle_i}{\int w( \mathbf{r} )dv}
}
$$

The denominator of this equation is the integral of the kernel in the whole region, excluding a central part occupied by particle $i$.

### Fluid density $\langle \rho \rangle_i$

Assuming that the particles **have the same mass** $m$ , the fluid density, $\langle \rho \rangle_i$ is expressed as,

$$
\eqalign{
\langle \rho \rangle_i = m\langle N \rangle_i = \frac{m\langle n \rangle_i}{\int w( \mathbf{r} )dv}
} 
$$

In the MPS method a fluid is represented by moving particles with constant mass. Thus, **the incompressibily of the fluid is guaranteed by keeping the particle number density** ($\langle n \rangle_i$) **of the fluid constant.** The continuity equation is also satisfied automatically by keeping the total number of particles and the mass of individual particles constant.

* * *

Model of Mathematical Operator
------------------------------

Each mathematical operator acting on the arbitrary scalar $\phi$ and vector $\mathbf{u}$ at particle $i$ are defined as the particle interaction approximation as follows:

### Gradient operator

Represent by the weighted average of gradient vectors.

$$
\eqalign{  
\langle \nabla \phi \rangle_i = \frac{d}{n^0}\sum_{i \neq j}  
\frac{\phi_j-\phi_i}{| \mathbf{r} _j - \mathbf{r}_i |^2} \left(\mathbf{r} _j - \mathbf{r}_i \right)w\left( | \mathbf{r} _j - \mathbf{r}_i | \right )  
}
$$

where $d$ is the number of space dimensions, $n^0$ is a particle number density ﬁxed for incompressibility.

### Laplacian operator

Part of a quantity contained by a particle $i$ is distributed to neighboring particles $j$ using the weight function.

$$
\eqalign{  
\langle \nabla^2 \phi \rangle_i = \frac{2d}{\lambda n^0}\sum_{i \neq j}  
\left[\left(\phi_j-\phi_i\right) w\left( | \mathbf{r} _j - \mathbf{r}_i | \right)\right] 
} 
$$

where $\lambda$ is

$$
\eqalign{ 
\lambda = \frac{\int_{V} w(r)r^2 dv}{\int_{V} w(r) dv} = \frac{\sum_{i \neq j} w \left( | \mathbf{r}_j - \mathbf{r}_i | \right) | \mathbf{r}_ j - \mathbf{r}_i |^2 }{ \sum_{i \neq j} w \left( | \mathbf{r}_j - \mathbf{r}_i | \right) } 
}
$$.

### Divergence operator

$$
\eqalign{  
\langle \nabla \cdot \mathbf{u} \rangle_i = \frac{2d}{n^0}\sum_{i \neq j}  
\frac{ \left( \mathbf{u}_j - \mathbf{u}_i \right) \cdot\left(\mathbf{r} _j - \mathbf{r}_i \right)}{| \mathbf{r} _j - \mathbf{r}_i |^2} w\left( | \mathbf{r} _j - \mathbf{r}_i | \right )  
} 
$$

* * *

Step of Semi-implicit Algorithm
-------------------------------

*   **Initialize configuration of particles**:

$$\eqalign{\mathbf{u}_i^0, \mathbf{r}_i^0, P_i^0 } $$

*   **Calculate the intermediate velocity $\mathbf{u}_i^*$ from part of momentum equation.**

$$\eqalign{ \mathbf{u}_i^* = \mathbf{u}_i^n + \Delta t & \left( \nu \nabla^2 \mathbf{u}_i^n + \mathbf{f} \right) } $$

*   **Calculate the intermediate** **coordinates of particles, $\mathbf{r}_i^*$**.

$$ \eqalign{ \mathbf{r}_i^* = \mathbf{r}_i^n + \Delta t & \mathbf{u}_i^* } $$

*   **Compute intermediate particle number density $n^*$ by using intermediate particle locations**.

*   **Obtain pressure $P_i^{n+1}$ by solving pressure Poisson equation.**

$$ \eqalign{ \nabla^2 P_i^{n+1} = -\frac{\rho}{\Delta t^2}\frac{n_i^*-n^0}{n^0} } $$

*   **Finally, new velocity $\mathbf{u}_i^{n+1}$ and new coordinates of particles $\mathbf{r}_i^{n+1}$ are computed.**

$$ \eqalign{ \mathbf{u}_i^{n+1} = \mathbf{u}_i^* - \frac{ \Delta t }{\rho}\nabla P_i^{n+1} } $$

$$ \eqalign{ \mathbf{r}_i^{n+1} = \mathbf{r}_i^n + \Delta t & \mathbf{u}_i^{n+1} } $$

* * *

Build System of Linear Equations
--------------------------------

*   **Linear Equations of intermediate velocity $\mathbf{u}_i^*$**.

$$\eqalign{  
\mathbf{u}_i^* = \mathbf{u}_i^n + \Delta t & \left( \nu \frac{2d}{\lambda n^0}\sum_{i \neq j} \left[\left(\mathbf{u}^n_j-\mathbf{u}^n_i\right) w\left( | \mathbf{r} _j - \mathbf{r}_i | \right )\right] + \mathbf{f} \right)  
}$$

*   **Linear Equations of intermediate** **coordinates of particles, $\mathbf{r}_i^*$**.

$$
\eqalign{ \mathbf{r}_i^* = \mathbf{r}_i^n + \Delta t & \mathbf{u}_i^* } $$

*   **Linear Equations of pressure $P_i^{n+1}$ from pressure Poisson equation.**

$$
\eqalign{  
\frac{2d}{\lambda n^0}\sum_{i \neq j}  
\left[\left(P_j-P_i\right) w\left( | \mathbf{r} _j - \mathbf{r}_i | \right )\right]  
= -\frac{\rho}{\Delta t^2}\frac{n_i^*-n^0}{n^0}  
} $$

*   **Linear Equations of new velocity $\mathbf{u}_i^{n+1}$ and new coordinates of particles $\mathbf{r}_i^{n+1}$.**

$$
\eqalign{  
\mathbf{u}_i^{n+1} = \mathbf{u}_i^* - \frac{ \Delta t }{\rho}\frac{d}{n^0}\sum_{i \neq j}  
\frac{(P_i-P_j)\cdot\left(\mathbf{r} _j - \mathbf{r}_i \right)}{| \mathbf{r} _j - \mathbf{r}_i |^2} w\left( | \mathbf{r} _j - \mathbf{r}_i | \right )  
}$$

$$
\eqalign{ \mathbf{r}_i^{n+1} = \mathbf{r}_i^n + \Delta t & \mathbf{u}_i^{n+1} }
$$

* * *

*   Reference:

1.  [A stable moving-particle semi-implicit method for free surface flows](https://www.sciencedirect.com/science/article/pii/S0169598305001322)
2.  [Moving Particle Semi-Implicit Method](https://www.wire.tu-bs.de/OLDWEB/akeese/seminarWS01/talks/mps_paper.pdf)