---
title: Enhancement of MPS Method
tags:
  - Uncategorized
id: '2313'
---

Formula of MPS Method
---------------------

\[latex\] \\eqalign{  
\\langle \\nabla \\phi \\rangle\_i = \\frac{d}{n^0}\\sum\_{i \\neq j}  
\\frac{\\phi\_j-\\phi\_i}{| \\mathbf{r} \_j - \\mathbf{r}\_i |^2} \\left(\\mathbf{r} \_j - \\mathbf{r}\_i \\right)w\\left( | \\mathbf{r} \_j - \\mathbf{r}\_i | \\right )  
} \[/latex\]

Following Koshizuka et al. (1998), the pressure gradient is defined by replacing \[latex\]\\phi\_i\[/latex\] by the minimum value of \[latex\]\\phi\[/latex\] among the neighboring particles.

\[latex\] \\eqalign{  
\\langle \\nabla P \\rangle\_i = \\frac{d}{n^0}\\sum\_{i \\neq j}  
\\frac{P\_j- \\hat{ P \_i }}{| \\mathbf{r} \_j - \\mathbf{r}\_i |^2} \\left(\\mathbf{r} \_j - \\mathbf{r}\_i \\right)w\\left( | \\mathbf{r} \_j - \\mathbf{r}\_i | \\right )  
} \[/latex\]

where \[latex\]\\hat{ P \_i }\[/latex\] is the minimum value selected among the neighboring particles within the distance of \[latex\]r\_e\[/latex\].

CMPS - momentum conservation
----------------------------

By considering Newton's second law, the forces due to pressure gradient exerted between particle \[latex\]j\[/latex\] and \[latex\]i\[/latex\] are:

\[latex\] \\eqalign{  
\\mathbf{ A }^p\_{j \\rightarrow i} = \\frac{m\_i d}{\\rho\_i n^0}  
\\frac{P\_j- \\hat{ P \_i }}{| \\mathbf{r} \_j - \\mathbf{r}\_i |^2} \\left(\\mathbf{r} \_j - \\mathbf{r}\_i \\right)w\\left( | \\mathbf{r} \_j - \\mathbf{r}\_i | \\right )  
} \[/latex\]

\[latex\] \\eqalign{  
\\mathbf{ A } ^p\_{i \\rightarrow j} = \\frac{m\_j d}{\\rho\_j n^0}  
\\frac{P\_i- \\hat{ P \_j }}{| \\mathbf{r} \_i - \\mathbf{r}\_j |^2} \\left(\\mathbf{r} \_i - \\mathbf{r}\_j \\right)w\\left( | \\mathbf{r} \_i - \\mathbf{r}\_j | \\right )  
} \[/latex\]

To guarntee conservation in linear momentum, we need the forces between two particles have the **same magnitude** in **opposite directions**. We derive an [**anti-symmetric** equation for pressure gradient term](https://www.sciencedirect.com/science/article/abs/pii/S0378383908001646) to achieve it.

\[latex\] \\eqalign{ \\langle \\nabla P \\rangle\_i = \\frac{d}{n^0}\\sum\_{i \\neq j} \\frac{(P\_i+P\_j) - (\\hat{ P \_i }+ \\hat{ P \_j})}{| \\mathbf{r} \_j - \\mathbf{r}\_i |^2} \\left(\\mathbf{r} \_j - \\mathbf{r}\_i \\right)w\\left( | \\mathbf{r} \_j - \\mathbf{r}\_i | \\right ) } \[/latex\]

The MPS method modiﬁed by the above pressure gradient formulation is referred to as **CMPS** (Corrected MPS). Besides conservation of **linear momentum**, CMPS also lead to the exact conservation of **angular momentum** for the pressure interacting forces. Since the exact conservation of linear momentum is automatically guaranteed for the viscous forces. Consequently, in CMPS, linear momentum is exactly conserved, and exact conservation of angular momentum is satisfied in the pressure interacting forces.

MPS-HS - source term in PPE
---------------------------

The MPS-HS method applies a **higher order source term** for the PPE for enhancement of pressure calculation. The higher order source term has been derived by **applying a higher order accurate time differentiation** of particle number density (in 2D).

\[latex\]\\eqalign{\\frac{Dn}{Dt}=& \\sum\_{i \\neq j}\\frac{Dw( | \\mathbf{r}\_ j - \\mathbf{r}i |)}{Dt}=\\sum\_{i \\neq j}\\frac{Dw\_{ij}}{Dt} \\\\=& \\sum\_{i \\neq j}( \\frac{\\partial w\_{ij}}{\\partial r\_{ij}}\\frac{\\partial r\_{ij}}{\\partial x\_{ij}}\\frac{d x\_{ij}}{ dt}+ \\frac{\\partial w\_{ij}}{\\partial r\_{ij}}\\frac{\\partial r\_{ij}}{\\partial y\_{ij}}\\frac{d y\_{ij}}{ dt}) \\\\ =&\\sum\_{i \\neq j}\\frac{-r\_e}{r^3\_{ij}}(x\_{ij}u\_{ij}+ y\_{ij}v\_{ij} )}\[/latex\]

Therefore, the modified PPE with higher order source term would be obtained as:

\[latex\]\\eqalign{ \\nabla^2 P\_i^{n+1} = \\frac{\\rho}{n^0\\Delta t}\\left(\\frac{Dn}{Dt}\\right)^=-\\frac{\\rho}{n^0\\Delta t}\\left(\\sum\_{i \\neq j}\\frac{r\_e}{r^3\_{ij}}(x\_{ij}u\_{ij}+ y\_{ij}v\_{ij} )\\right)^\* } \[/latex\]

The standard MPS method modified by the above formulation is refered as **MPS-HS**.

MPS-HL - higher order Laplacian model in PPE
--------------------------------------------

\[refer 1\]: [https://www.sciencedirect.com/science/article/abs/pii/S0378383908001646](https://www.sciencedirect.com/science/article/abs/pii/S0378383908001646)