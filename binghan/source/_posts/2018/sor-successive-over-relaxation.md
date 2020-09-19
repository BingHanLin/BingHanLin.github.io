---
title: SOR (Successive Over - Relaxation)
tags:
  - Numerical Method
categories: 
  - Uncategorized
id: '183'
date: 2018-03-20 00:34:25
mathjax: true
---

Introduction
------------

The **successive overrelaxation method (SOR)** is one of the stationary iterative methods for solving a linear system of equations( \[latex\]\\bf A\\bf x=\\bf b\[/latex\] ). The four main stationary methods are the **Jacobi method**, **Gauss-Seidel method**, successive overrelaxation method (SOR), and symmetric successive overrelaxation method (SSOR). The SOR can be derived from the Gauss-Seidel method with a plus parameter \[latex\]\\omega\[/latex\]. It could converge faster than Gauss-Seidel method when a proper \[latex\]\\omega\[/latex\] is chosen.

* * *

Jacobi Method
-------------

In this methods, a set of initial guessed values is used for solving each unknown variable in the linear system. The computed values are then used in the next iteration level. The process is repeated until the computed values reach the state of convergence. Therefore, the new value of \[latex\]x\_i\[/latex\] at the new iteration \[latex\]k+1\[/latex\] level can be computed from,

\[latex\]\\eqalign{ x^{k+1}\_i=(b\_i-\\sum\_{j=1}^{i-1}a\_{ij}x^k\_j-\\sum\_{j=i+1}^{n}a\_{ij}x^k\_j)/a\_{ii} \\quad i = 1,2,3...,n. }\[/latex\]

where \[latex\] a,~x,~b \[/latex\] are the elements in matrix \[latex\]\\bf A \[/latex\], column vector \[latex\] \\bf x\[/latex\] and \[latex\] \\bf b \[/latex\] respectively. Then \[latex\]\\bf A \[/latex\] can be further decomposed into a diagonal component \[latex\]\\bf D \[/latex\], the strictly lower triangular component \[latex\]-\\bf L \[/latex\], and strictly upper triangular component  \[latex\]-\\bf U \[/latex\]. The equation can be written as,

\[latex\]\\eqalign{\\bf A = \\bf D - \\bf L - \\bf U }\[/latex\]

The definition of the Jacobi method now can be expressed with matrices as,

\[latex\]\\eqalign{\\bf x^{k+1}=\\bf D^{-1}(\\bf L+\\bf U)+\\bf D^{-1}\\bf b}\[/latex\]

One may immediately notice a way to improve procedure by using the newly computed values to obtain the \[latex\]\\bf x^{k+1}\[/latex\] once they are available. Indeed, implementation of this idea becomes the Gauss-Seidel iteration method, which has better convergence rate. The Jacobi method is rarely used in practice due to it low convergence rate, but it provides a good basis for developing the advanced methods.

* * *

Gauss-Seidel Method
-------------------

The Gauss-Seidel method (called Seidel's method) can be applied to any matrix with non-zero elements on the diagonals. The method is convergent if the largest elements are located in the main diagonal of the coefficient matrix. The formula for the Gauss-Seidel method is extremely similar to that of the Jacobi matrix,

\[latex\]\\eqalign{x^{k+1}\_i=(b\_i-\\sum\_{j=1}^{i-1}a\_{ij}x^{k+1}\_j-\\sum\_{j=i+1}^{n}a\_{ij}x^k\_j)/a\_{ii} \\quad i = 1,2,3...,n.}\[/latex\]

, but each component of the new iterate depends upon all previously computed value. Unlike the Jacobi method, only one storage vector is required during the computation, which can be advantageous for solving very large problems. Again, the Gauss-Seidel method can be expressed with matrices as,

\[latex\]\\eqalign{\\bf x^{k+1}=\\bf D^{-1}(\\bf b + \\bf L\\bf x^{k+1}+\\bf U\\bf x^{k})}\[/latex\]

or,

\[latex\]\\eqalign{\\bf x^{k+1}=(\\bf D-\\bf L)^{-1}\\bf U \\bf x^{k}+(\\bf D - \\bf L)^{-1} \\bf b}\[/latex\]

In the next section, an extrapolation factor \[latex\]\\omega\[/latex\] will be added into the equations of the Gauss-Seidel method, which gives us the Successive Overrelaxation method.

* * *

Successive Overrelaxation Method
--------------------------------

The method of successive over-relaxation (SOR) is derived by extrapolating the Gauss-Seidel method. It takes the form of a weighted average between the previous iterate and the computed Gauss-Seidel iterate successively for each component,

\[latex\]\\eqalign{x^{k+1}\_i =\\omega \\overline{x} ^{k+1}\_i + (1-\\omega)x^{k}\_i}\[/latex\]

where \[latex\]\\overline{x}\[/latex\] denote the component computed from Gauss-Seidel method and \[latex\]\\omega\[/latex\] is the extrapolation factor called the relaxation factor ( \[latex\]\\omega> 1\[/latex\] ). The element basis formula can be written as,

\[latex\]\\eqalign{x^{k+1}\_i=x^k\_i + \\omega(b\_i-\\sum\_{j=1}^{i-1}a\_{ij}x^{k+1}\_j-\\sum\_{j=i+1}^{n}a\_{ij}x^k\_j)/a\_{ii} \\quad i = 1,2,3...,n}\[/latex\]

In matrix terms, the SOR algorithm is written as,

\[latex\]\\eqalign{\\bf x^{k+1}=(\\bf D-\\omega\\bf L)^{-1}\[(1-\\omega) \\bf D+\\omega \\bf U \] \\bf x^{k}+\\omega(\\bf D - \\omega\\bf L)^{-1} \\bf b}\[/latex\]

If \[latex\]\\omega = 1\[/latex\], the SOR method simplifies to the Gauss-Seidel method. The choice of relaxation factor \[latex\]\\omega\[/latex\] is not necessarily easy, and depends upon the properties of the coefficient matrix. Frequently, some heuristic estimate is used, such as \[latex\]\\omega=2-O(h)\[/latex\] where \[latex\]h\[/latex\] is the mesh spacing of the discretization of the underlying physical domain. In general, SOR fails to converge if  \[latex\]\\omega\[/latex\] is outside the interval \[latex\] (0,2) \[/latex\].

* * *

Python code and comparison
--------------------------

In this section, we realize the procedure by python code and compare the three algorithms mentioned above. The following numerical procedure considers a simple linear equation \[latex\]\\bf A\\bf x=\\bf b\[/latex\]  and iterates to produce the solution vector. The linear equation is define as,

\[latex\]\\eqalign{\\bf A = \\begin{bmatrix}4 & 3 & 0\\\\3 & 4 & -1\\\\0 & -1 & 4\\end{bmatrix}, \\quad \\bf b = \\begin{bmatrix}24 \\\\30\\\\-24\\end{bmatrix}}\[/latex\]

with the solution vector

\[latex\]\\eqalign{\\bf x = \\begin{bmatrix}3 \\\\4\\\\-5\\end{bmatrix}}\[/latex\]

The relative iteration convergence tolerance is set as \[latex\]10^{-6}\[/latex\] and the relaxation factor \[latex\]\\omega\[/latex\] is chosen to be 1.25. The python code is demonstrated as follow: \[python\] # Solves linear equation systems such as Ax=b using # 1. Jacobi Method # 2. Gauss-Seidel Method Method # 3. SOR Successive Over-Relaxation Method # 2017.08.13 Bing Han, Lin import math import matplotlib.pyplot as plt import numpy as np def solver(A, Xstar, b, flag, omg=1, max\_iter=100, max\_tol=10e-6): err = \[\] D = np.diag(np.diag(A)) L = -np.tril(A, -1) U = -np.triu(A, 1) if (flag==1): B = np.mat( np.linalg.inv( D ) ) \* np.mat( L + U ) f = np.mat( np.linalg.inv( D ) ) \* np.mat(b) elif (flag==2): omg = 1 B = np.mat( np.linalg.inv( D - omg \* L ) )\* np.mat( ((1 - omg) \* D + omg \* U) ) f = omg \* np.mat(np.linalg.inv( D - omg \* L )) \* np.mat(b) elif (flag==3): B = np.mat( np.linalg.inv( D - omg \* L ) )\* np.mat( ((1 - omg) \* D + omg \* U) ) f = omg \* np.mat(np.linalg.inv( D - omg \* L )) \* np.mat(b) for i in range(max\_iter): Xnew = B\*Xstar + f err.append( np.linalg.norm( Xnew - Xstar, 1) ) Xstar = Xnew if (err\[i\] <= max\_tol): break return Xnew, err if \_\_name\_\_ == '\_\_main\_\_': A = np.matrix(\[\[4, 3, 0\], \[3, 4, -1\],\[0, -1, 4\]\]) b = np.matrix(\[24, 30, -24\]).transpose() omg = 1.25 # relaxation factor max\_iter = 1000 # maximum number of iteration max\_tol = 10e-6 # maximum tolerance of convergence error Xstar = np.zeros\_like(b) # initial assumption of solution vector Xnew1, err1 = solver(A, Xstar, b, 1, 1, max\_iter, max\_tol) Xnew2, err2 = solver(A, Xstar, b, 2, 1, max\_iter, max\_tol) Xnew3, err3 = solver(A, Xstar, b, 3, 1.25, max\_iter, max\_tol) # plot figure plt.style.use('bmh') fig, ax1 = plt.subplots(figsize=(10, 5), dpi=100, facecolor='w', edgecolor='k') plt.tick\_params(labelsize = 16) font = {'family': 'serif', 'color': 'black', 'weight': 'normal', 'size': 16, } ax1.plot(err1, 'r', marker='o', markersize=8, label = 'Jacobi Method') ax1.plot(err2, 'g', marker='d', markersize=8, label = 'Gauss-Seidel Method') ax1.plot(err3, 'b', marker='^', markersize=8, label = 'SOR Method') ax1.grid(True) ax1.set\_yscale('log') ax1.set\_xlabel('Number of Iterations', fontdict=font) ax1.set\_ylabel('Convergence Error in log Scale', fontdict=font) plt.legend( borderaxespad= 2) plt.show() print ('Complete!') \[/python\] The solution vectors computed from each algorithm are listed in the table:

 

Jacobi Method

Gauss-Seidel Method

SOR Method

exact sol

\[latex\] x\_1 \[/latex\]

3.00000141

3.00000592

2.99999871

3

\[latex\] x\_2 \[/latex\]

4.00000165

3.99999507

4.00000049

4

\[latex\] x\_3 \[/latex\]

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

From the table, we can tell that the number of iterations different, as that of the Successive-Over Relaxation method has 11 iterations, Gauss - Seidel method has 26  iterations, while Jacobi method has 62 iterations. The absolute error of the solution vectors is very small for all three algorithms that the difference can be neglected. This shows that Successive-Over Relaxation requires less computer storage than the Gauss - Seidel and Jacobi method. Thus, the Successive-Over Relaxation could be considered more efficient of the three methods.

* * *

*   Reference:

1.  [mathworld.wolfram](http://mathworld.wolfram.com/SuccessiveOverrelaxationMethod.html)
2.  [Wikipedia](https://en.wikipedia.org/wiki/Successive_over-relaxation)
3.  [MAA](https://www.maa.org/press/periodicals/loci/joma/iterative-methods-for-solving-iaxi-ibi-the-sor-method)
4.  [数值分析-逐次超松弛迭代法PPT](http://www.1mpi.com/doc/fb800b0896e3113d780382f2/7)
5.  [Linear Equations & Iterative Methods](http://www.southampton.ac.uk/~feeg6002/lecturenotes/feeg6002_numerical_methods01.html)