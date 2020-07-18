---
title: '[Reading Notes] Python Machine Learning – 02'
tags:
  - Machine Learning
  - Python Machine Learning - 2018
id: '1079'
date: 2018-06-30 00:32:29
---

> June 2018, Chapter 2.

* * *

Artificial Neurons
------------------

An artificial neuron is a **mathematical function** conceived as a model of biological neurons, an **artificial neural network (ANN)**. Artificial neurons are elementary units in an artificial neural network. The artificial neuron **receives one or more inputs** (representing excitatory postsynaptic potentials and inhibitory postsynaptic potentials at neural dendrites) and sums them to **produce an output** (or activation, representing a neuron's action potential which is transmitted along its axon).

* * *

The early history of artificial neurons
---------------------------------------

The first artificial neuron was first proposed by Warren McCulloch and Walter Pitts in 1943. It employed a **threshold**, equivalent to using the Heaviside step function. Initially, only a simple model was considered, with binary inputs and outputs, some restrictions on the possible weights, and a more flexible threshold value. Frank Rosenblatt, using the McCulloch-Pitts neuron and the findings of Hebb, went on to develop the first perceptron. This **perceptron**, which could learn through the weighting of inputs, was instrumental in the later formation of neural networks.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/-4-e1529568376146.png)

  
_Artificial Neurons ( Source : [python-machine-learning-book](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynbm) )_

* * *

How does it work?
-----------------

We use a binary classification task to show how artificial neurons work. Given an input, the output neuron fires (produces an output of 1) only if the data point belongs to the target class. Otherwise, it does not fire (it produces an output of -1). We use a unit step function \[latex\]\\boldsymbol{\\phi}\[/latex\] (also called Heaviside step function) as activation function. The definition of the sign function:

\[latex\] \\phi(z)= \\left\\{ \\begin{aligned} &1 \\quad \\textrm{if} \\quad z\\geq \\theta\\\\ &-1 \\quad \\textrm{otherwise} \\end{aligned} \\right. \[/latex\]

where \[latex\]\\theta\[/latex\] is the threshold, and \[latex\]z\[/latex\] is the net input which is the specified linear combination of input vector \[latex\]\\boldsymbol{x}\[/latex\] and the coressponding weighting coefficients vector \[latex\]\\boldsymbol{w}\[/latex\], i.e., ( \[latex\]z = w\_1 x\_1 + \\dotsc + w\_m x\_m\[/latex\]).

\[latex\] \\boldsymbol{x} = \\begin{bmatrix}x\_1 \\\\ \\vdots \\\\ x\_m \\end{bmatrix}, \\quad \\boldsymbol{w} = \\begin{bmatrix}w\_1 \\\\ \\vdots \\\\ w\_m \\end{bmatrix} \[/latex\]

For simplicity's sake, we let \[latex\]w\_0 = -\\theta\[/latex\] and \[latex\]x\_0 = 1\[/latex\]. Then, \[latex\]z\[/latex\] can be redefined as \[latex\]z = w\_0 x\_0 + w\_1 x\_1 + \\dotsc + w\_m x\_m = \\boldsymbol{w}^T\\boldsymbol{x}\[/latex\]. The activation function \[latex\]\\phi(z)\[/latex\] can also be rewritten as

\[latex\]  
\\phi(z)=  
\\left\\{  
\\begin{aligned}  
&1 \\quad \\textrm{if} \\quad z\\geq 0\\\\  
&-1 \\quad \\textrm{otherwise}  
\\end{aligned}  
\\right.  
\[/latex\]

The figure below shows how the net input \[latex\]z\[/latex\] is used to classify the linearly separable datas in a binary classification task.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/圖片2.png)

  
_Source : [python-machine-learning-book](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynbm)_

The processes of this artificial neurons can be summarized as follow:

1.  Initialize the weighting coefficients \[latex\]\\boldsymbol{w}\[/latex\] to all zeros or small random number.
2.  Do the following steps for every training set \[latex\]\\boldsymbol{x}^{(i)}\[/latex\]:  
    a. Calculate the predict value \[latex\]\\hat{y}^{(i)}\[/latex\]  
    b. Update the weighting coefficients \[latex\]\\boldsymbol{w}\[/latex\]. 

The weighting coefficients \[latex\]\\boldsymbol{w}\[/latex\] could be updated by the following equation. The processes of this artificial neurons can be summarized as follow:

\[latex\]  
\\eqalign{  
w\_j\\mathrel{\\mathop:}= w\_j+ \\Delta w\_j;\\qquad  
\\Delta w\_j = \\eta( y^{(i)} - \\hat{y}^{(i)})x^{(i)}\_j  
}  
\[/latex\]

\[latex\]  
\\eqalign{  
w\_j\\mathrel{\\mathop:}= w\_j+ \\Delta w\_j;\\qquad  
\\Delta w\_j = \\eta( y^{(i)} - \\hat{y}^{(i)})x^{(i)}\_j  
}  
\[/latex\]

where \[latex\]\\eta\[/latex\] is **learning rate** (a small constant from 0 to 1), \[latex\]y^{(i)}\[/latex\] is the target variable that we are trying to predict, and \[latex\]\\hat{y}^{(i)}\[/latex\] is the value we predict by our model.

Before we show you a simple Python code to carry out all of these processes, an animation is shown below to visualize the steps we mentioned.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/Perceptron_training_without_bias.gif)

  
_Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Perceptron_training_without_bias.gif)_

* * *

Implementing PLA in Python
--------------------------

The flow chart for the perceptron learning algorithm is shown as below.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/-2-1-e1529591898950.png)

  
_Source: [python-machine-learning-book](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynbm)_

First, a class is created for **perceptron**. We can create a perceptron instance by giving learning rate \[latex\]\\eta\[/latex\] and the **number of iterations** (epochs) with this class. The _fit_ method is used for training the perceptron to adapt our data. Once you finish the training, the _predict_ method can be used the predict the result of a new data.

    [python]
    import numpy as np
    
    class Perceptron(object):
    
    
        def __init__(self, eta=0.01, n_iter=10):
            self.eta = eta
            self.n_iter = n_iter
    
    
        def fit(self, X, y):
            self.w_ = np.zeros(1 + X.shape[1])
            self.errors_ = []
    
            for _ in range(self.n_iter):
                errors = 0
                for xi, target in zip(X, y):
                    update = self.eta * (target - self.predict(xi))
                    self.w_[1:] += update * xi
                    self.w_[0] += update
                    errors += int(update != 0.0)
                self.errors_.append(errors)
            return self
    
    
        def net_input(self, X):
            """Calculate net input"""
            return np.dot(X, self.w_[1:]) + self.w_[0]
    
    
        def predict(self, X):
            """Return class label after unit step"""
            return np.where(self.net_input(X)= 0.0, 1, -1)
    [/python]

_Refer [here](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynb) for completed code_

* * *

Case Study:  Iris dataset
-------------------------

Here, we get the iris dataset from online respository and make a label vector \[latex\]y\[/latex\] for **Iris-virginica** and **Iris-setosai**.  The features of the iris dataset are given to \[latex\]X\[/latex\].

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
    
    # plot data
    plt.scatter(X[:50, 0], X[:50, 1],
                color='red', marker='o', label='setosa')
    plt.scatter(X[50:100, 0], X[50:100, 1],
                color='blue', marker='x', label='versicolor')
    
    plt.xlabel('sepal length [cm]')
    plt.ylabel('petal length [cm]')
    plt.legend(loc='upper left')
    
    plt.tight_layout()
    
    #plt.savefig('./images/02_06.png', dpi=300)
    plt.show()
    [/python]

_Refer [here](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynb) for completed code_

Let's look at the distribution of these 100 iris dataset. Our target is to find a possible decision boundary to identify the region for these two kinds of iris dataset.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/09/下載.png)

  
_  
Distribution of iris dataset. (Source :  [python-machine-learning-book)](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynbm)_

With the operation below, the perceptron can be trained to fit our data. Furthermore, we could plot a figure to show the **number of misclassifications** in each **iteration (epochs)**. It shows that the algorithm converges in the sixth iteration and the perceptron separate our training dataset perfectly!

    [python]
    ppn = Perceptron(eta=0.1, n_iter=10)
    
    ppn.fit(X, y)
    
    plt.plot(range(1, len(ppn.errors_) + 1), ppn.errors_, marker='o')
    plt.xlabel('Epochs')
    plt.ylabel('Number of updates')
    
    plt.tight_layout()
    # plt.savefig('./perceptron_1.png', dpi=300)
    plt.show()
    [/python]

_Refer [here](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynb) for completed code_

![](https://bhlin.co.network/wp/wp-content/uploads/2018/09/下載-1.png)

  
_Source :  [python-machine-learning-book](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynbm)_

At last, the result can be visualize as following. The detail of this process can also be found [here](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynb).

![](https://bhlin.co.network/wp/wp-content/uploads/2018/09/下載-2.png)

  
_Source :  [python-machine-learning-book](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynbm)_

* * *

Summary
-------

In this reading note we give a brief introduction to **artificial neurons** and apply a simple perceptron to dealing with a binary classification problem.

* * *

*   Reference:

1.  [Artificial Neuron](https://en.wikipedia.org/wiki/Artificial_neuron)
2.  [History of the Perceptron](https://web.csulb.edu/~cwallis/artificialn/History.htm)
3.  [Artificial Neural Networks: Linear Classification](http://briandolhansky.com/blog/2013/7/11/artificial-neural-networks-linear-classification-part-2)  
    
4.   [Python Machine Learning - Code Examples](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynb)  
    
5.   [Developing a Machine Learning Model from Start to Finish](https://medium.com/@yaelg/product-manager-guide-part-3-developing-a-machine-learning-model-from-start-to-finish-c3e12fd835e4)