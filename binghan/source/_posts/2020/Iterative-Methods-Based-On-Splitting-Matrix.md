---
title: Iterative Methods Based On Splitting Matrix
tags:
  - Numerical Method
categories: 
  - Uncategorized
date: 2020-10-04 09:00:36
mathjax: true
---

Introduction
------------

Consider the linear equation system

$$
\eqalign{\mathbf{Ax = b} }
$$

where $\mathbf{A} \in \mathcal{R}^{n \times n}$ is a nonsigular matrix and $\mathbf{x}$ , $\mathbf{b} \in \mathcal{R}^{n}$.

A large class of iterative methods for solving linear equation system involve splitting the matrix $\mathbf{A}$ into the difference between two new matrices $\mathbf{S}$ and $\mathbf{T}$ :

<!-- more -->

$$
\eqalign{\mathbf{A} = \mathbf{S-T} } \text{, with S nonsingular.}
$$

This gives us

$$
\eqalign{\mathbf{Sx} = \mathbf{Tx+b} }, \label{eq1} \tag{1}
$$

and the approximate solution $\mathbf{x}^{k+1}$ can be found as following

$$
\eqalign{\mathbf{Sx}^{k+1} = \mathbf{Tx}^{k} + \mathbf{b} }, \label{eq2} \tag{2}
$$

The iterative methods start from an initail guess $\mathbf{x}^{0}$ and produce better approximations $\mathbf{x}^{1}$, $\mathbf{x}^{2}$, $\cdots$ . If this procedure converges, i.e. $\mathbf{x}^{k+1} \rightarrow \mathbf{x}$, $k \rightarrow \infty$, then $\mathbf{x}^{k+1}$ solve the original problem.

If the diagonal entries of the matrix $\mathbf{A}$ are all nonzero, and we express the matrix $\mathbf{A}$ as

$$
\eqalign{\mathbf{A} = \mathbf{D+L+U} }
$$

where $\mathbf{D}$ is the diagonal part, $\mathbf{L}$ is strictly lower triangular matrix and $\mathbf{U}$ is strictly upper triangular matrix. We can then defined three standard iterative schemes ad follows:

* **Jabobi meshod**  $\mathbf{S=D}, \mathbf{T=-(L+U)}$;

* **Gauss-Seidel method**  $\mathbf{S=L+D}, \mathbf{T=-U}$;

* **Successive over-relaxation(SOR) method** a combination of above methods.

* * *
Jabobi Method
-------------

In this methods, $\mathbf{S}$ is simply the diagonal part of $\mathbf{A}$. Rewrite equation [2](#mjx-eqn-eq2) give us

$$
\eqalign{\mathbf{Dx}^{k+1} = -(\mathbf{L}+\mathbf{U})\mathbf{x}^{k}+\mathbf{b}  }.  
$$

With the known values $\mathbf{x}^{k}$ in preivous iteration level $k$, the computed values $\mathbf{x}^{k+1}$ is obtained in current iteration level $k+1$. The process is repeated until the computed values reach the state of convergence.

One may immediately notice a way to improve procedure by using the newly computed values to obtain the $\mathbf x^{k+1}$ once they are available. Indeed, implementation of this idea becomes the Gauss-Seidel method, which has better convergence rate. The Jacobi method is rarely used in practice due to it **low convergence rate**, but it provides a good basis for developing the advanced methods.

```julia Jacobi Method
function jacobi(mat::Array{Float64,2}, sol::Array{Float64,1}, rhs::Array{Float64,1},
                maxIter::Int=100, tol::Float64=1.0e-8)

    nbrows, nbcols = size(mat)
    result = deepcopy(sol)
    residuals = Array{Float64,1}(undef, 0)

    
    numIter = 0
    while numIter < maxIter
        numIter+=1
        
        deltaSol = rhs - mat*result
        
        for i=1:nbrows
            deltaSol[i] = deltaSol[i]/mat[i,i]
        end
        
        result = result + deltaSol
        
        nrm = norm(deltaSol)
        
        push!(residuals,nrm)
        
        if nrm <= tol
            return result, numIter, residuals
        end
    end

    return result, numIter, residuals
end
```

* * *
Gauss-Seidel Method
-------------------

Besides **low convergence rate**,  Jacobi method requires us to store all the components of
$\mathbf x^{k}$ until we have finished computing the next iteration $\mathbf x^{k+1}$. To overcome these drawbacks, Gauss-Seidel Method use the **new** values of $\mathbf{x}$ as soon as we have calculated them. Again, rewrite equation [2](#mjx-eqn-eq2) give us

$$
\eqalign{(\mathbf{D+L})\mathbf{x}^{k+1} = -\mathbf{U}\mathbf{x}^{k}+\mathbf{b} }.  
$$

Each component of the current iteration level depends upon all previously computed value. Unlike the Jacobi method, **only one storage vector is required during the computation** in practice, which can be advantageous for solving very large problems. In the next section, an extrapolation factor $\omega$ will be added into the equations of the Gauss-Seidel method, which gives us the Successive Over-Relaxation method.

```julia Gauss-Seidel Method
function gaussSeidel(mat::Array{Float64,2}, sol::Array{Float64,1}, rhs::Array{Float64,1},
                maxIter::Int=100, tol::Float64=1.0e-8)

    nbrows, nbcols = size(mat)
    result = deepcopy(sol)
    deltaSol = deepcopy(sol)
    residuals = Array{Float64,1}(undef, 0)

    
    numIter = 0
    while numIter < maxIter
        
        numIter+=1
        
        for i=1:nbrows
            oldResult = result[i]
            result[i] = rhs[i]
            
            for j=1:nbcols
                if i!=j
                    result[i]-=mat[i,j]*result[j]
                end
            end
            result[i]/=mat[i,i]
            
            deltaSol[i]=result[i]-oldResult
        end
        
        nrm = norm(deltaSol)
        
        push!(residuals,nrm)
        
        if nrm <= tol
            return result, numIter, residuals
        end
        
    end
    return result, numIter, residuals
end
```

* * *
Successive Over-Relaxation Method(SOR)
-------------------------------------

In iterative methods, we assume that the direction from $\mathbf x^{k}$ to $\mathbf x^{k+1}$ is taking us closer to the true solution. Then it would make sense to **move further along the direction** $(\mathbf{x}^{k+1}-\mathbf{x}^{k})$. This key concept lead us to Successive Over-Relaxation(SOR) method which is derived by extrapolating the Gauss-Seidel method.

Let us rearrange Gauss-Seidel equation as

$$
\eqalign{\mathbf{x^{k+1} = D^{-1}\left[-Lx^{k+1}-Ux^{k}+b\right] } }.  
$$

Subtract $\mathbf x^{k}$ from both sides to get

$$
\eqalign{\mathbf{x^{k+1} - x^{k} = D^{-1}\left[-Dx^{k+1}-Lx^{k+1}-Ux^{k}+b\right] } }.  
$$

As mentioned above, the idea of the **SOR method** is to iterate by moving further along the direction $(\mathbf{x}^{k+1}-\mathbf{x}^{k})$.

$$
\eqalign{\mathbf{x}^{k+1} = \mathbf{x}^{k} -\omega(\mathbf{x}^{k+1}-\mathbf{x}^{k}) }.  
$$

Written out in detail, the SOR Method is

$$
\eqalign{\mathbf{x^{k+1} = x^{k} + \omega D^{-1}\left[-Lx^{k+1}-Ux^{k}+b\right] } }.  
$$
 
Finally, the **SOR method** can be written as,

$$
\eqalign{
    (\mathbf{D}+\omega\mathbf{L})\mathbf{x}^{k+1} =\left[(1-\omega)\mathbf{D}-\omega\mathbf{U}\right]\mathbf{x}^k+\omega\mathbf{b}
}
$$

If $\omega = 1$, the **SOR method** simplifies to the Gauss-Seidel method. The choice of relaxation factor $\omega$ is not necessarily easy, and depends upon the properties of the coefficient matrix. Frequently, some heuristic estimate is used, such as $\omega=2-O(h)$ where $h$ is the mesh spacing of the discretization of the underlying physical domain. In general $\omega$ is inside the interval $ (1,2) $.

```julia Successive Over-Relaxation Method
function SOR(mat::Array{Float64,2}, sol::Array{Float64,1}, rhs::Array{Float64,1}, omega::Float64,
                maxIter::Int=100, tol::Float64=1.0e-8)

    nbrows, nbcols = size(mat)
    result = deepcopy(sol)
    deltaSol = deepcopy(sol)
    residuals = Array{Float64,1}(undef, 0)

    
    numIter = 0
    while numIter < maxIter
        
        numIter+=1

        for i=1:nbrows
            oldResult = result[i]
            result[i] = rhs[i]
            
            for j=1:nbcols
                if i!=j
                    result[i]-=mat[i,j]*result[j]
                end
            end
            
            result[i]*=omega
            result[i]/=mat[i,i]
            result[i]+=(1-omega)*oldResult
            
            deltaSol[i]=result[i]-oldResult
        end
        
        nrm = norm(deltaSol)
        push!(residuals,nrm)
        
        if nrm <= tol
            return result, numIter, residuals
        end
        
    end
    return result, numIter, residuals
end
```

* * *

*   Reference:

1.  [Iterative method](https://en.wikipedia.org/wiki/Iterative_method)
2.  [Iterative methods for matrix equations](http://www.it.uom.gr/teaching/linearalgebra/ExamplesToIterativeMethods.pdf
)
3.  [Iterative Methods: The SOR Method](https://www.maa.org/press/periodicals/loci/joma/iterative-methods-for-solving-iaxi-ibi-the-sor-method)
3.  [Iterative Methods for System of Equations](https://slideplayer.com/slide/4787543/)

