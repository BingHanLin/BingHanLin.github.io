---
title: Solving Differential Equations by Neural Networks
tags:
  - Machine Learning
categories: 
  - Machine Learning
id: '1825'
date: 2019-05-18 19:17:20
mathjax: true
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

$$
\eqalign{ \frac{\mathrm{d}\Psi}{\mathrm{d}x}=f(x,\Psi) .}
$$  

Same with the traditional numerical method, we obtain the numerical solution of \$\Psi(x)$ on a set of grids. The solution is approximated on each grid (node) with neural network architecture, therefore, we have **one input neuron** (or two input neurons for 2D problems), one hidden layer, and **one output neuron** to predict solution (scalar value) of the differential equation on each grid. The architecture of the neural network look likes this:

![](https://i.imgur.com/GSxyuba.png)

Schematic of NN.

Take initial (IC) or boundary (BC) conditions into account, we choose a form for the trial function $\Psi_t$ such that satisfies the ICs or BCs. This is achieved by writing it as a sum of two terms:

$$
\eqalign{  
\Psi_t(\vec{x})=A(\vec{x})+F(\vec{x},N(\vec{x},\vec{p})).  
}
$$

Where $N(\vec{x},\vec{p})$ is a **single-output feedforward neural network** with parameters (weights and biases) $\vec{p}$ and n (depents on the dimension of the problem) input units fed with the input vector $\vec{x}$, the first term $A(\vec{x})$ contains no adjustable parameters and satisfies the ICs or BCs, and the second term $F$ is constructed so as not to contribute to the ICs or BCs (give zero on those positions).

Since the trial function $\Psi_t$ satisfies the ICs or BCs, the rest of work is to adjusted weights and biases makes $\Psi_t$ satisfies the governing equations. Thus, the problem is transformed into a minimization problem as follow:  

$$
\eqalign{ E \left[ \vec{p} \right]= \sum_i\left[{ \frac{\mathrm{d}\Psi(x_i)}{\mathrm{d}x}-f(x_i,\Psi_t(x_i)) } \right]^2 }
$$

where the $x_i$ are locations of each grid. The target of our **neural network** is to optimize the parameters to minimize the function above, so-called **loss function**. For the detail of the python code, please refer to [here](https://github.com/BingHanLin/My_ML_Notes/tree/master/Neural%20Networks%20for%20Differential%20Equations).

### Example

With the acknowledge above, we consider the example of first order ODE to illustrate the method:

$$
\eqalign{ \frac{d\Psi}{dx}+(x+\frac{1+3x^2}{1+x+x^3})\Psi=x^3+2x+x^2\frac{1+3x^2}{1+x+x^3}} 
$$

and

$$
\eqalign{ x \in \left[ 0,1 \right], \quad \Psi(0)=1 .} 
$$  

The trial solution $\Psi_t$ is written as

$$
\eqalign{ \Psi_t(\vec{x})=1+xN(\vec{x},\vec{p}) .}
$$

Thus, $\frac{\mathrm{d}\Psi(x)}{\mathrm{d}x}$ can be obtained easily:

$$
\eqalign{\frac{\mathrm{d} \Psi(x)}{\mathrm{d}x} = N(\vec{x}) + x\frac{\mathrm{d} N(\vec{x})}{\mathrm{d}x} .}
$$

In this example, we used a multilayer perceptron having one hidden layer with 10 hidden units and one linear output unit. The activate function of each hidden unit is chosen to be the sigmoid function:

$$
\eqalign{\sigma(x) = \frac{1}{1+e^{-x}} }
$$

The analytic solution of this problem is:

$$
\Psi_{a}(x) = \frac{e^{-x^2}/2}{1+x+x^3}  
$$

We set up a grid in the range $\left[ 0, 1 \right]$ with 10 nodes and train our **neural network** on these locations. Result of training the neural network for 1000 iterations is shown in the figure below:

![](https://i.imgur.com/y3tE8ad.png)

Result of predict solution from the neural network.

The result could be improved by many ways such as adding more grid points, adding more neurons in the hidden layer, etc. But this is out of the scope of this post. For the detail of the python code, please refer to [here](https://github.com/BingHanLin/My_ML_Notes/tree/master/Neural%20Networks%20for%20Differential%20Equations).

* * *

Partial Differential Equation
-----------------------------

There is no difference between the processes for solving ODEs and PDEs by this method. Only the number of the **input neuron** needs to be changed (two or more input neurons) according to the problems.

### Example

Consider the following PDE :

$$
\nabla{\Psi}^2(x,y) = e^{-x}(x-2+y^3+6y)
$$

and,  

$$
x,y \in \left[ 0,1 \right] 
$$

$$
\Psi(0,y) = y^3, \quad \Psi(1,y) = (1+y^3)e^{-1}
$$

$$
\Psi(x,0) = xe^{-x}, \quad \Psi(x,1) = (x+1)e^{-x}
$$

The trial solution which satisfies the constraints above is assumed to be:

$$
\Psi_t(x,y) = A(x,y)+x(1-x)y(1-y)N(x,y,\vec{p})
$$

where $A(x,y)$ is defined below:

$$
\eqalign{A(x,y) =& (1-x)y^3+x(1+y^3)e^{-1}+(1-y)x(e^{-x}-e^{-1}) \\ &+y\left[ (1+x)e^{-x}-(1-x-2xe^{-1}) \right] }
$$

The analytic solution of this problem is:

$$
\eqalign{\Psi_{a}(x, y) = e^{-x}(x+y^3)}
$$

We set up a mesh grid in the range of $x,y \in \left[ 0,1 \right] $ with 100 uniform distribution points. Result of training the neural network for 500 iterations is shown in the figure below:

![](https://i.imgur.com/AQkB43d.png)

Result of predict solution from the neural network.

For the detail of the python code, please refer to [here](https://github.com/BingHanLin/My_ML_Notes/tree/master/Neural%20Networks%20for%20Differential%20Equations).

* * *

*   Reference:

1.  [Artificial Neural Networks for Solving Ordinary and Partial Differential Equations](https://arxiv.org/pdf/physics/9705023.pdf), I. E. Lagaris, A. Likas and D. I. Fotiadis, 1997
2.  [Neural networks for solving differential equations](https://becominghuman.ai/neural-networks-for-solving-differential-equations-fa230ac5e04c), Alexandr Honchar, 2017