---
title: Solving Differential Equations by Neural Networks
tags:
  - Machine Learning
  - Machine learning and data mining
id: '1825'
date: 2019-05-18 19:17:20
---

Neural networks have been used for solving many problems such as sales forecasting, customer research, data validation, and risk management. As an universal function approximators, Neural networks can learn (fit) patterns from data with the complicated distribution. With the same concept, train a Neural network to fit the differential equations could also be possible. In this post, I want to show how to applied a simple feed-forward NNs to solve differential equations (ODE, PDE).

The theoretical details and computational implementations are inspired by the following paper and blog. For those who interest in the more details, please refer to these links:

1.  [Artificial Neural Networks for Solving Ordinary and Partial Differential Equations](https://arxiv.org/pdf/physics/9705023.pdf), I. E. Lagaris, A. Likas and D. I. Fotiadis, 1997
2.  [Neural networks for solving differential equations](https://becominghuman.ai/neural-networks-for-solving-differential-equations-fa230ac5e04c), Alexandr Honchar, 2017

Different from the works in Alexandr Honchar's post, I reimplement the computational process with **Tensorflow** - a popular deep learning framework developed by Google. 

* * *

Ordinary Differential Equation
------------------------------

Let's start with a simple ordinary differential equation (ODE) in the form of

\[latex\] \\eqalign{ \\frac{\\mathrm{d}\\Psi}{\\mathrm{d}x}=f(x,\\Psi) } \[/latex\].  

Same with the traditional numerical method, we obtain the numerical solution of \[latex\] \\Psi(x)\[/latex\] on a set of grids. The solution is approximated on each grid (node) with neural network architecture, therefore, we have **one input neuron** (or two input neurons for 2D problems), one hidden layer, and **one output neuron** to predict solution (scalar value) of the differential equation on each grid. The architecture of the neural network look likes this:

![](https://bhlin.co.network/wp/wp-content/uploads/2019/05/NNs-1024x710.png)

Schematic of NN.

Take initial (IC) or boundary (BC) conditions into account, we choose a form for the trial function \[latex\] \\Psi\_t\[/latex\] such that satisfies the ICs or BCs. This is achieved by writing it as a sum of two terms:

\[latex\] \\eqalign{  
\\Psi\_t(\\vec{x})=A(\\vec{x})+F(\\vec{x},N(\\vec{x},\\vec{p}))  
} \[/latex\].

Where \[latex\] N(\\vec{x},\\vec{p}) \[/latex\] is a **single-output feedforward neural network** with parameters (weights and biases) \[latex\] \\vec{p} \[/latex\] and n (depents on the dimension of the problem) input units fed with the input vector \[latex\] \\vec{x} \[/latex\], the first term \[latex\] A(\\vec{x})\[/latex\] contains no adjustable parameters and satisfies the ICs or BCs, and the second term \[latex\] F \[/latex\] is constructed so as not to contribute to the ICs or BCs (give zero on those positions).

Since the trial function \[latex\] \\Psi\_t\[/latex\] satisfies the ICs or BCs, the rest of work is to adjusted weights and biases makes \[latex\] \\Psi\_t\[/latex\] satisfies the governing equations. Thus, the problem is transformed into a minimization problem as follow:  

\[latex\]\\eqalign{ E\[\\vec{p}\] = \\sum\_i\\left\[{ \\frac{\\mathrm{d}\\Psi(x\_i)}{\\mathrm{d}x}-f(x\_i,\\Psi\_t(x\_i)) } \\right\]^2 }\[/latex\]

where the \[latex\]x\_i \[/latex\] are locations of each grid. The target of our **neural network** is to optimize the parameters to minimize the function above, so-called **loss function**. For the detail of the python code, please refer to [here](https://github.com/BingHanLin/My_ML_Notes/tree/master/Neural%20Networks%20for%20Differential%20Equations).

### Example

With the acknowledge above, we consider the example of first order ODE to illustrate the method:

\[latex\] \\eqalign{ \\frac{d\\Psi}{dx}+(x+\\frac{1+3x^2}{1+x+x^3})\\Psi=x^3+2x+x^2\\frac{1+3x^2}{1+x+x^3}} \[/latex\],  

and

\[latex\] \\eqalign{ x \\in \[0,1\], \\quad \\Psi(0)=1 } \[/latex\].  

The trial solution \[latex\] \\Psi\_t\[/latex\] is written as

\[latex\] \\eqalign{ \\Psi\_t(\\vec{x})=1+xN(\\vec{x},\\vec{p}) }\[/latex\].

Thus, \[latex\]\\frac{\\mathrm{d}\\Psi(x)}{\\mathrm{d}x} \[/latex\] can be obtained easily:

\[latex\] \\eqalign{\\frac{\\mathrm{d} \\Psi(x)}{\\mathrm{d}x} = N(\\vec{x}) + x\\frac{\\mathrm{d} N(\\vec{x})}{\\mathrm{d}x} } \[/latex\].

In this example, we used a multilayer perceptron having one hidden layer with 10 hidden units and one linear output unit. The activate function of each hidden unit is chosen to be the sigmoid function:

\[latex\] \\eqalign{\\sigma(x) = \\frac{1}{1+e^{-x}} } \[/latex\]

The analytic solution of this problem is:

\[latex\] \\Psi\_{a}(x) = \\frac{e^{-x^2}/2}{1+x+x^3}  
\[/latex\]

We set up a grid in the range \[0, 1\] with 10 nodes and train our **neural network** on these locations. Result of training the neural network for 1000 iterations is shown in the figure below:

![](https://bhlin.co.network/wp/wp-content/uploads/2019/05/ANN_for_ODE.png)

Result of predict solution from the neural network.

The result could be improved by many ways such as adding more grid points, adding more neurons in the hidden layer, etc. But this is out of the scope of this post. For the detail of the python code, please refer to [here](https://github.com/BingHanLin/My_ML_Notes/tree/master/Neural%20Networks%20for%20Differential%20Equations).

* * *

Partial Differential Equation
-----------------------------

There is no difference between the processes for solving ODEs and PDEs by this method. Only the number of the **input neuron** needs to be changed (two or more input neurons) according to the problems.

### Example

Consider the following PDE :

\[latex\] \\nabla{\\Psi}^2(x,y) = e^{-x}(x-2+y^3+6y)\[/latex\]

and,  

\[latex\] x,y \\in \[0,1\] \[/latex\]

\[latex\] \\Psi(0,y) = y^3, \\quad \\Psi(1,y) = (1+y^3)e^{-1} \[/latex\]

\[latex\] \\Psi(x,0) = xe^{-x}, \\quad \\Psi(x,1) = (x+1)e^{-x} \[/latex\]

The trial solution which satisfies the constraints above is assumed to be:

\[latex\] \\Psi\_t(x,y) = A(x,y)+x(1-x)y(1-y)N(x,y,\\vec{p}) \[/latex\]

where \[latex\] A(x,y) \[/latex\] is defined below:

\[latex\] \\eqalign{A(x,y) =& (1-x)y^3+x(1+y^3)e^{-1}+(1-y)x(e^{-x}-e^{-1}) \\\\ &+y\[(1+x)e^{-x}-(1-x-2xe^{-1})\] } \[/latex\]

The analytic solution of this problem is:

\[latex\] \\eqalign{\\Psi\_{a}(x, y) = e^{-x}(x+y^3)} \[/latex\]

We set up a mesh grid in the range of \[latex\] x,y \\in \[0,1\] \[/latex\] with 100 uniform distribution points. Result of training the neural network for 500 iterations is shown in the figure below:

![](https://bhlin.co.network/wp/wp-content/uploads/2019/05/ANN_for_PDE.png)

Result of predict solution from the neural network.

For the detail of the python code, please refer to [here](https://github.com/BingHanLin/My_ML_Notes/tree/master/Neural%20Networks%20for%20Differential%20Equations).

* * *

*   Reference:

1.  [Artificial Neural Networks for Solving Ordinary and Partial Differential Equations](https://arxiv.org/pdf/physics/9705023.pdf), I. E. Lagaris, A. Likas and D. I. Fotiadis, 1997
2.  [Neural networks for solving differential equations](https://becominghuman.ai/neural-networks-for-solving-differential-equations-fa230ac5e04c), Alexandr Honchar, 2017