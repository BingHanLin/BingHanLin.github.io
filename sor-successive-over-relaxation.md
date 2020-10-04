---
title: Iterative Methods Based On Splitting Matrix
tags:
  - Numerical Method
categories: 
  - Uncategorized
id: '183'
date: 2020-09-26 00:34:25
mathjax: true
---

Introduction
------------

Iterative methods start from an initail guess $x_0$ and 

A matrix splitting is an expression which represents a given matrix as a sum or difference of matrices. 


All the methods we will consider involve splitting the matrix



The **successive overrelaxation method (SOR)** is one of the stationary iterative methods for solving a linear system of equations ($\bf{Ax}=\bf{b}$). The four main stationary methods are the **Jacobi method**, **Gauss-Seidel method**, **successive overrelaxation method** (SOR), and **symmetric successive overrelaxation method** (SSOR). The SOR can be derived from the Gauss-Seidel method with a plus parameter $\omega$. It could converge faster than Gauss-Seidel method when a proper $\omega$ is chosen.
<!-- more -->

<!-- * * *

Jacobi Method
-------------

In this methods, a set of initial guessed values is used for solving each unknown variable in the linear system. The computed values are then **used in the next iteration level**. The process is repeated until the computed values reach the state of convergence. Therefore, the new value of $x_i$ at the new iteration $k+1$ level can be computed from,

$$
\eqalign{ x^{k+1}_i=(b_i-\sum_{j=1}^{i-1}a_{ij}x^k_j-\sum_{j=i+1}^{n}a_{ij}x^k_j)/a_{ii} \quad i = 1,2,3...,n. }
$$

where $a$, $x$ and $b$ are the elements in matrix $\bf{A}$, column vector $\bf{x}$ and $\bf{b}$ respectively. Then $\bf{A}$ can be further decomposed into a diagonal component $\bf{D}$, the strictly lower triangular component $\bf{L}$, and strictly upper triangular component $\bf{U}$. The equation can be written as,

$$
\eqalign{\bf{A} = \bf{D} + \bf{L} + \bf{U} }
$$

The definition of the Jacobi method now can be expressed with matrices as,

$$
\eqalign{\bf x^{k+1}=\bf{D^{-1}(-L-U)x^{k}}  + \bf{D^{-1}b} }
$$

One may immediately notice a way to improve procedure by using the newly computed values to obtain the $\bf x^{k+1}$ once they are available. Indeed, implementation of this idea becomes the Gauss-Seidel iteration method, which has better convergence rate. The Jacobi method is rarely used in practice due to it low convergence rate, but it provides a good basis for developing the advanced methods.

* * *

Gauss-Seidel Method
-------------------

The Gauss-Seidel method (called Seidel's method) can be applied to any matrix with non-zero elements on the diagonals. The method is convergent if the largest elements are located in the main diagonal of the coefficient matrix. The formula for the Gauss-Seidel method is extremely similar to that of the Jacobi matrix,

$$
\eqalign{x^{k+1}_i=(b_i-\sum_{j=1}^{i-1}a_{ij}x^{k+1}_j-\sum_{j=i+1}^{n}a_{ij}x^k_j)/a_{ii} \quad i = 1,2,3...,n.}
$$

Each component of the new iterate depends upon all previously computed value. Unlike the Jacobi method, **only one storage vector is required during the computation**, which can be advantageous for solving very large problems. Again, the Gauss-Seidel method can be expressed with matrices as,

$$
\eqalign{\bf{ x^{k+1}=(D+L)^{-1}(-U)x^{k} + (D+L)^{-1}b }}
$$

In the next section, an extrapolation factor $\omega$ will be added into the equations of the Gauss-Seidel method, which gives us the Successive Overrelaxation method.

* * *

Successive Overrelaxation Method
--------------------------------

The method of successive over-relaxation (SOR) is derived by extrapolating the Gauss-Seidel method. It takes the form of a weighted average between the previous iterate and the computed Gauss-Seidel iterate successively for each component,

$\eqalign{x^{k+1}_i =\omega \overline{x} ^{k+1}_i + (1-\omega)x^{k}_i}$

where $\overline{x}$ denote the component computed from Gauss-Seidel method and $\omega$ is the extrapolation factor called the relaxation factor ( $\omega> 1$ ). The element basis formula can be written as,

$\eqalign{x^{k+1}_i=x^k_i + \omega(b_i-\sum_{j=1}^{i-1}a_{ij}x^{k+1}_j-\sum_{j=i+1}^{n}a_{ij}x^k_j)/a_{ii} \quad i = 1,2,3...,n}$

In matrix terms, the SOR algorithm is written as,

$\eqalign{\bf x^{k+1}=(\bf D-\omega\bf L)^{-1}\[(1-\omega) \bf D+\omega \bf U \] \bf x^{k}+\omega(\bf D - \omega\bf L)^{-1} \bf b}$

If $\omega = 1$, the SOR method simplifies to the Gauss-Seidel method. The choice of relaxation factor $\omega$ is not necessarily easy, and depends upon the properties of the coefficient matrix. Frequently, some heuristic estimate is used, such as $\omega=2-O(h)$ where $h$ is the mesh spacing of the discretization of the underlying physical domain. In general, SOR fails to converge if  $\omega$ is outside the interval $ (0,2) $.

* * *

Python code and comparison
--------------------------

In this section, we realize the procedure by python code and compare the three algorithms mentioned above. The following numerical procedure considers a simple linear equation $\bf A\bf x=\bf b$  and iterates to produce the solution vector. The linear equation is define as,

$\eqalign{\bf A = \begin{bmatrix}4 & 3 & 0\\3 & 4 & -1\\0 & -1 & 4\end{bmatrix}, \quad \bf b = \begin{bmatrix}24 \\30\\-24\end{bmatrix}}$

with the solution vector

$\eqalign{\bf x = \begin{bmatrix}3 \\4\\-5\end{bmatrix}}$

The relative iteration convergence tolerance is set as $10^{-6}$ and the relaxation factor $\omega$ is chosen to be 1.25. The python code is demonstrated as follow: \[python\] # Solves linear equation systems such as Ax=b using # 1. Jacobi Method # 2. Gauss-Seidel Method Method # 3. SOR Successive Over-Relaxation Method # 2017.08.13 Bing Han, Lin import math import matplotlib.pyplot as plt import numpy as np def solver(A, Xstar, b, flag, omg=1, max_iter=100, max_tol=10e-6): err = \[\] D = np.diag(np.diag(A)) L = -np.tril(A, -1) U = -np.triu(A, 1) if (flag==1): B = np.mat( np.linalg.inv( D ) ) \* np.mat( L + U ) f = np.mat( np.linalg.inv( D ) ) \* np.mat(b) elif (flag==2): omg = 1 B = np.mat( np.linalg.inv( D - omg \* L ) )\* np.mat( ((1 - omg) \* D + omg \* U) ) f = omg \* np.mat(np.linalg.inv( D - omg \* L )) \* np.mat(b) elif (flag==3): B = np.mat( np.linalg.inv( D - omg \* L ) )\* np.mat( ((1 - omg) \* D + omg \* U) ) f = omg \* np.mat(np.linalg.inv( D - omg \* L )) \* np.mat(b) for i in range(max_iter): Xnew = B\*Xstar + f err.append( np.linalg.norm( Xnew - Xstar, 1) ) Xstar = Xnew if (err\[i\] <= max_tol): break return Xnew, err if __name__ == '__main__': A = np.matrix(\[\[4, 3, 0\], \[3, 4, -1\],\[0, -1, 4\]\]) b = np.matrix(\[24, 30, -24\]).transpose() omg = 1.25 # relaxation factor max_iter = 1000 # maximum number of iteration max_tol = 10e-6 # maximum tolerance of convergence error Xstar = np.zeros_like(b) # initial assumption of solution vector Xnew1, err1 = solver(A, Xstar, b, 1, 1, max_iter, max_tol) Xnew2, err2 = solver(A, Xstar, b, 2, 1, max_iter, max_tol) Xnew3, err3 = solver(A, Xstar, b, 3, 1.25, max_iter, max_tol) # plot figure plt.style.use('bmh') fig, ax1 = plt.subplots(figsize=(10, 5), dpi=100, facecolor='w', edgecolor='k') plt.tick_params(labelsize = 16) font = {'family': 'serif', 'color': 'black', 'weight': 'normal', 'size': 16, } ax1.plot(err1, 'r', marker='o', markersize=8, label = 'Jacobi Method') ax1.plot(err2, 'g', marker='d', markersize=8, label = 'Gauss-Seidel Method') ax1.plot(err3, 'b', marker='^', markersize=8, label = 'SOR Method') ax1.grid(True) ax1.set_yscale('log') ax1.set_xlabel('Number of Iterations', fontdict=font) ax1.set_ylabel('Convergence Error in log Scale', fontdict=font) plt.legend( borderaxespad= 2) plt.show() print ('Complete!') \[/python\] The solution vectors computed from each algorithm are listed in the table:

 

Jacobi Method

Gauss-Seidel Method

SOR Method

exact sol

$ x_1 $

3.00000141

3.00000592

2.99999871

3

$ x_2 $

4.00000165

3.99999507

4.00000049

4

$ x_3 $

\-5.00000047

\-5.00000123

\-4.99999957

\-5

Number of iterations

62

26

11

 

Absolute error

2.59E-06

2.4E-07

3.7E-07

 

And the convergence error over iterations are plotted here.

![Alt text](https://bhlin.co.network/wp/wp-content/uploads/2018/03/Figure_1-6.png)

From the table, we can tell that the number of iterations different, as that of the Successive-Over Relaxation method has 11 iterations, Gauss - Seidel method has 26  iterations, while Jacobi method has 62 iterations. The absolute error of the solution vectors is very small for all three algorithms that the difference can be neglected. This shows that Successive-Over Relaxation requires less computer storage than the Gauss - Seidel and Jacobi method. Thus, the Successive-Over Relaxation could be considered more efficient of the three methods. -->

* * *

*   Reference:

1.  [mathworld.wolfram](http://mathworld.wolfram.com/SuccessiveOverrelaxationMethod.html)
2.  [Wikipedia](https://en.wikipedia.org/wiki/Successive_over-relaxation)
3.  [MAA](https://www.maa.org/press/periodicals/loci/joma/iterative-methods-for-solving-iaxi-ibi-the-sor-method)
4.  [数值分析-逐次超松弛迭代法PPT](http://www.1mpi.com/doc/fb800b0896e3113d780382f2/7)
5.  [Linear Equations & Iterative Methods](http://www.southampton.ac.uk/~feeg6002/lecturenotes/feeg6002_numerical_methods01.html)