---
title: '[Reading Notes] Python Machine Learning – 01'
tags:
  - Machine Learning
  - Python Machine Learning - 2018
id: '880'
date: 2018-06-11 01:40:40
---

> June 2018, Chapter 1.

* * *

Types of machine learning Algorithms
------------------------------------

Broadly, Machine Learning Algorithmscan be divided into 3 categories according to their purpose: (1) supervised learning, (2) reinforcement learning, and (3) unsupervised learning.

![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/1_9Eu_-DDMZ_bP_t94_MMEYA.png ) Source : Analytics vidhya

1.  **Supervised Learning** The main goal in supervised learning is to learn a model from **labeled training data** that allows us to make predictions about unseen or future data. Algorithms try to model relationships and dependencies between the target prediction output and the input features by generate a function with weighting coefficients from the training data sets. The training process continues until the model achieves a desired level of accuracy on the training data. The main types of supervised learning problems include **classification** and **regression** problems.
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/-e1528647632870.png ) Supervised Learning (Source : https://github.com/rasbt/python-machine-learning-book)
    
    **_\- Classification:_** This is a type of problem where we predict the categorical response value where the data can be separated into specific “classes” (ex: we predict one of the values in a set of values). Some examples are: this mail is spam or not? will it rain today or not? is this picture a cat or a dog or a tiger? (multi-class classification) **_\- Regression:_** This is a type of problem where we need to predict the continuous-response value (ex : above we predict number which can vary from -infinity to +infinity) Some examples are: what is the price of house in a specific city? what is the value of the stock? how many total runs can be on board in a cricket game? **_Notes:_**
    
    *   With labeled data
    *   Main problems include regression and classification problems
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/圖片1.png) Left: classification, Right: regression (Source : https://www.kdnuggets.com/2017/11/3-different-types-machine-learning.html)
    
    * * *
    
2.  **Reinforcement Learning** Reinforcement learning algorithm (called the agent) continuously learns from the environment in an iterative fashion. In the process, the agent learns from its experiences of the environment until it explores the full range of possible states. Since the information about the current state of the environment typically also includes a so-called reward signal, we can think of reinforcement learning as a field related to supervised learning.However, in reinforcement learning this feedback is not the correct ground truth label or value, but a measure of how well the action was measured by a reward function. This method aims at using observations gathered from the interaction with the environment to take actions that would maximize the reward or minimize the risk. A popular example of reinforcement learning is a chess engine. Here, the agent decides upon a series of moves depending on the state of the board (the environment), and the reward can be defined as win or lose at the end of the game.
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/-1-e1528649589936.png ) Reinforcement Learning (Source : https://github.com/rasbt/python-machine-learning-book)
    
    **_Notes:_**
    
    *   Continuously learns from the environment
    *   Includes a so-called reward signal
    
    * * *
    
3.  **Unsupervised Learning** In supervised learning, we know the right answer beforehand when we train our model, and in reinforcement learning, we define a measure of reward for particular actions by the agent. In unsupervised learning, however, we are dealing with **unlabeled data or data of unknown structure**. Using unsupervised learning techniques, we are able to explore the structure of our data to extract meaningful information without the guidance of a known outcome variable or reward function. **_\- Clustering_** Clustering is an exploratory data analysis technique that allows us to organize a pile of information into meaningful subgroups (clusters) without having any prior knowledge of their group memberships. Clustering is a great technique for structuring information and deriving meaningful relationships from data. For example, it allows marketers to discover customer groups based on their interests, in order to develop distinct marketing programs.
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/-1-1-e1528650695415.png) Clustering (Source : https://github.com/rasbt/python-machine-learning-book)
    
    **_\- Compressing Data via Dimensionality Reduction_** Another subfield of unsupervised learning is dimensionality reduction. Often we are working with data of high dimensionality—each observation comes with a high number of measurements—that can present a challenge for limited storage space and the computational performance of machine learning algorithms. Unsupervised dimensionality reduction is a commonly used approach in feature preprocessing to remove noise from data, which can also degrade the predictive performance of certain algorithms, and compress the data onto a smaller dimensional subspace while retaining most of the relevant information.
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/-2-e1528650769947.png) Compressing Data via Dimensionality Reduction (Source : https://github.com/rasbt/python-machine-learning-book)
    
    **_Notes:_**
    *   Without labeled data
    *   Explore the structure of the data

* * *

A roadmap for building machine learning systems
-----------------------------------------------

*   **Preprocessing - getting data into shape** The goal of this phase is to collect raw data and get it into a form that can be plugged as an input into your prototype model. You may need to perform complex transformations on the data to achieve that. This usually includes the following works:
    *   Collect data for your prototype
    *   Data cleanup and normalization
    *   Compressing Data via Dimensionality Reduction See this [website](https://medium.com/@yaelg/product-manager-guide-part-3-developing-a-machine-learning-model-from-start-to-finish-c3e12fd835e4) for further details.
*   **Training and selecting a predictive model** The goal of this stage is to get to a prototype of a model, test it and iterate on it until you get to a model that gives good enough results to be ready for production.
    
*   **Evaluating models and predicting unseen data instances** You get to this stage when you decide that your prototype model works well enough to address your business problem and can be launched in production.
    
    ![](https://bhlin.co.network/wp/wp-content/uploads/2018/06/下載-3.png) Roadmap for building machine learning systems (Source : https://github.com/rasbt/python-machine-learning-book)
    

* * *

*   Reference:

1.  [Python Machine Learning - Code Examples](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch02/ch02.ipynb)
2.  [David Fumo](https://towardsdatascience.com/types-of-machine-learning-algorithms-you-should-know-953a08248861)
3.  [Madhu Sanjeevi ( Mady )](https://medium.com/deep-math-machine-learning-ai/different-types-of-machine-learning-and-their-types-34760b9128a2)
4.  [Essentials of Machine Learning Algorithms](https://www.analyticsvidhya.com/blog/2017/09/common-machine-learning-algorithms/)
5.  [3 different types of machine learning](https://www.kdnuggets.com/2017/11/3-different-types-machine-learning.html)
6.  [Developing a Machine Learning Model from Start to Finish](https://medium.com/@yaelg/product-manager-guide-part-3-developing-a-machine-learning-model-from-start-to-finish-c3e12fd835e4)