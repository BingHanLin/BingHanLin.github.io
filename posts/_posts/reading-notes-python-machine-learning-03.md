---
title: '[Reading Notes] Python Machine Learning – 03'
tags:
  - Machine Learning
  - python
  - Python Machine Learning - 2018
id: '1384'
date: 2018-10-23 00:45:56
---

> September 2018, Chapter 2.

* * *

Adaptive Linear Neurons
-----------------------

Adaline linear neuron can be regarded as an improvement over the oldest and simplest perceptron(McCulloch–Pitts neuron). Instead of using  Heaviside step function as activation function like in MCP, adaptive linear neurons use a linear activation function to get the continuous-valued output. This activation function \[latex\] \\phi\[/latex\] can be written as

  
\[latex\] \\phi(z)= \\phi(  
\\boldsymbol{ w}^T  
\\boldsymbol{x}) =  
\\boldsymbol{ w}^T   
\\boldsymbol{x} \[/latex\]

We can compare both learning algorithms in the figure illustrated below.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/10/MCP_Adaline.png)

  
_Source : [python-machine-learning-book](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynbm)_

* * *

Cost function & Gradient descent
--------------------------------

The next step is to use the continuous-valued output from the linear activation function to compute the model error and update the weights. Before doing that, we need to measure how well our model fit into the data. Thus, we define the **cost function** \[latex\]\\ \\boldsymbol{J}\[/latex\] which is expressed as

  
\[latex\] \\boldsymbol{J(w)}=\\frac{1}{2}\\sum\_i\\left( y^{(i)} -\\phi(z^  
{(i)} )\\right)^2\[/latex\]

  
this equation indicates the **sum of squared errors (SSE)** between the **output value** and the **actual output**. The **SSE** is halved \[latex\] \\frac{1}{2}\[/latex\] as a convenience for the computation of the gradient descent. To ensure our model fits into the data, we need to estimate a set of weightings which minimizing **cost functions** \[latex\] \\ \\boldsymbol{J}\[/latex\]. That's where **gradient descent** comes in. The equations below show how gradient descent algorithm is used to update the weightings \[latex\] \\ \\boldsymbol{w}\[/latex\]:

\[latex\] \\boldsymbol{w}:=\\boldsymbol{w}+\\Delta\\boldsymbol{w}  
\[/latex\]

where

\[latex\] \\Delta\\boldsymbol{w}=-\\eta \\ \\nabla\\boldsymbol{J(w)}  
\[/latex\]

The equation for updating  each weighting \[latex\] \\ w\_j\[/latex\] is shown below.

\[latex\]\\eqalign{ \\begin{aligned} w\_j =& w\_j+\\Delta w\_j\\\\=& w\_j-\\eta\\frac{\\partial\\boldsymbol{J}}{\\partial w\_j}\\\\=&w\_j+\\eta\\sum\_i(y^{(i)} -\\phi(z^{(i)} ))x^{(i)}\_j \\end{aligned}}\[/latex\]

Note that at each iteration j, one should simultaneously update the weightings  \[latex\] \\ w\_0, \\ w\_2, \\ ....\\, w\_m\[/latex\]. See [here](https://medium.freecodecamp.org/understanding-gradient-descent-the-most-popular-ml-algorithm-a66c0d97307f) and [here](https://towardsdatascience.com/gradient-descent-algorithm-and-its-variants-10f652806a3) for more detail of the gradient descent algorithm.

* * *

Implementing in Python
----------------------

Again, we create a class for **Adaptive Linear Neurons**. We can create a perceptron instance by giving learning rate \[latex\]\\eta\[/latex\] and the **number of iterations** (epochs) with this class.

    [python]
    class AdalineGD(object):
     
        def __init__(self, eta=0.01, n_iter=50):
            self.eta = eta
            self.n_iter = n_iter
    
        def fit(self, X, y):
            self.w_ = np.zeros(1 + X.shape[1])
            self.cost_ = []
    
            for i in range(self.n_iter):
                output = self.activation(X)
                errors = (y - output)
                self.w_[1:] += self.eta * X.T.dot(errors)
                self.w_[0] += self.eta * errors.sum()
                cost = (errors**2).sum() / 2.0
                self.cost_.append(cost)
    
            return self
    
        def net_input(self, X):
            """Calculate net input"""
            return np.dot(X, self.w_[1:]) + self.w_[0]
    
        def activation(self, X):
            """Compute linear activation"""
            return self.net_input(X)
    
        def predict(self, X):
            """Return class label after unit step"""
            return np.where(self.activation(X) >= 0.0, 1, -1)
    [/python]

 _Refer [here](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynb) for completed code_

* * *

Case Study:  Iris dataset
-------------------------

The same dataset we studied in [**perceptron**](http://arning-02/?preview_id=1079&preview_nonce=5a5861ceaa&preview=true#Implementing_PLA_in_Python) is used to show how **Adaptive Linear Neurons** work. 

    [python]
    import matplotlib.pyplot as plt
    import numpy as np
    import pandas as pd
    
    # read in iris data from online respository
    df = pd.read_csv('https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data', header=None)
    
    # select setosa and versicolor
    y = df.iloc[0:100, 4].values
    y = np.where(y == 'Iris-setosa', -1, 1)
    
    # extract sepal length and petal length
    X = df.iloc[0:100, [0, 2]].values
    
    
    fig, ax = plt.subplots(nrows=1, ncols=2, figsize=(8, 4))
    
    # training with larger learning rate
    ada1 = AdalineGD(n_iter=10, eta=0.01).fit(X, y)
    ax[0].plot(range(1, len(ada1.cost_) + 1), np.log10(ada1.cost_), marker='o')
    ax[0].set_xlabel('Epochs')
    ax[0].set_ylabel('log(Sum-squared-error)')
    ax[0].set_title('Adaline - Learning rate 0.01')
    
    # training with smaller learning rate
    ada2 = AdalineGD(n_iter=10, eta=0.0001).fit(X, y)
    ax[1].plot(range(1, len(ada2.cost_) + 1), ada2.cost_, marker='o')
    ax[1].set_xlabel('Epochs')
    ax[1].set_ylabel('Sum-squared-error')
    ax[1].set_title('Adaline - Learning rate 0.0001')
    
    plt.tight_layout()
    plt.show()
    
    [/python]

The figures below show us the cost function (**SSE)** in each Epoch under two different learning rate. Figure on the right shows the cost function decrease as the number of epoch increases. But due to the small learning rate, it needs many epochs before cost function become convergent. While figure on the left shows cost function increase as the number of iteration increases due to the big learning rate.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/10/下載.png)

  
_(Source :  [python-machine-learning-book)](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynbm)_

We can see what happened during the training for two different learning rate from the figure below. To ensure our model obtain the **global cost minimum**, we should choose a proper learning rate during the training. Besides the adjustment of learning rate, some preprocessing data technique, such as feature scaling, also help us train the model better. ([see here for example](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynb))

![](https://bhlin.co.network/wp/wp-content/uploads/2018/10/下載-1.png)

  
  
_Left: small learning rate; _Right: big learning rate._ (Source :  [python-machine-learning-book)](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynbm)_  

* * *

Summary
-------

*   With the implementation of **Adaptive Linear Neurons**, the gradient descent algorithm can be used to update the weightings.
*   The learning rate \[latex\]\\eta\[/latex\] need to be chosen properly.
*   When we deal with the large-scale machine learning problem, the **stochastic gradient descent (SGD)** might be a more efficient method to train the model. (see [here](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynb) for the detail of SGD implementation)

* * *

*   Reference:

1.  [Python Machine Learning - Code Examples](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynb)
2.  [How to understand Gradient Descent, the most popular ML algorithm](https://medium.freecodecamp.org/understanding-gradient-descent-the-most-popular-ml-algorithm-a66c0d97307f)
3.  [Gradient Descent Algorithm and Its Variants](https://towardsdatascience.com/gradient-descent-algorithm-and-its-variants-10f652806a3)