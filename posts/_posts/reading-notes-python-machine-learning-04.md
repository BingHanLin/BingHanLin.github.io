---
title: '[Reading Notes] Python Machine Learning – 04'
tags:
  - Machine Learning
  - Python Machine Learning - 2018
id: '949'
date: 2018-12-13 12:33:15
---

> November 2018, Chapter 4. (Data Pre-Processing)

* * *

Deal with Missing Values
------------------------

We need to understand that in real-world machine learning problems are fraught with **missing data**. Dataset can have missing values for a number of reasons such as observations that were not recorded and data corruption. Before we start building and training a model, missing values must be carefully handled at the first step.   
  
Here are some common ways of dealing with missing data:  
  

*   **Deletion**

The simplest strategy for handling missing data is to remove records that contain a missing value. This can be done either **listwise**, where the rows that contain any missing data are deleted, or **pairwise**, where the missing data is simply ignored and the variables that are present are considered. 　Additionally, sometimes you can **drop variables** if the data is missing for more than 60% records but only if that variable is insignificant.  
  
Since these approaches and the method of deletion lead to loss of information, this methodology is used only when the deletion of some data will not substantially affect the overall system.   
  

*   **Replacement**

If the missing values belong to a numeric field like the age of a person or the ticket fare, the values can be statistically replaced.  These missing values can be filled by the **mean** or **mode** or **median** of the present values in the dataset. This approximation will surely add variance to the dataset, but there will be no loss of information in this case.  
  
Another way is to approximate it with the deviation of neighbouring values. This works better if the data is linear.    
  

*   **Predictive Imputation**

Imputing refers to using a model to replace missing values. Regression techniques can be employed to accomplish treatment of missing values in the dataset by predictive imputation. Many other algorithms can also be tried to identify the one that yields the correct predictions.   
  

*   **Assigning An Unique Category**

A categorical feature, such as gender, will have a definite number of possibilities. Since they have a definite number of classes, we can assign another class for the missing values.

* * *

Handling categorical data
-------------------------

Dealing with numeric data is often easier than categorical data due to the additional complexities of the semantics pertaining to each category value. The categorical data need some amount of **transformations** before we can start modeling on our data.  
  
We have to further distinguish between **nominal** and **ordinal** features.  Ordinal features can be understood as categorical values that can be sorted or ordered (e.g. Size of the T-shirt). In contrast, nominal features don't imply any order (e.g. Color of the T-shirt).   
  

*   **Label Encoding**

Label encoding is simply converting each value in a column to a number. Label encoding has the advantage that it is straightforward but it has the disadvantage that the model will **misunderstand** the data to be in some kind of order, such as 0 < 1 < 2. But this isn’t the case data with nominal categorical attributes. To overcome this problem, we use One Hot Encoding.  
  

*   **One Hot Encoding**

The strategy of one hot encoding is to convert each category value into a new column and assigns a **1 or 0 (True/False)** value to the column. This has the benefit of not weighting a value improperly but does have the downside of adding more columns to the data set. There are even more advanced algorithms for categorical encoding. For those who interesting in it, please refer to [here](http://pbpython.com/categorical-encoding.html) and [here](https://towardsdatascience.com/understanding-feature-engineering-part-2-categorical-data-f54324193e63).

* * *

Split data in training and test sets
------------------------------------

To train and test the performance of our model, we need to divide our dataset into two subsets:

*   **training set** — the dataset that we use to train the model (weights and biases in the case of Neural Network). The model sees and learns from this data.
*   **test set** — a subset to evaluate the trained model. It is only used once a model is completely trained.

Make sure that your test set meets the following two conditions:

*   Is large enough to yield statistically meaningful results.
*   Is representative of the data set as a whole. In other words, don't pick a test set with different characteristics than the training set.

* * *

Feature Scaling
---------------

Our dataset often contain features highly varying in magnitudes. For most of machine learning algorithms, the features with high magnitudes will weigh in a lot more in the distance calculations than features with low magnitudes. To supress this effect, we need to **bring all features to the same level of magnitudes**. This can be acheived by feature scaling.   
  
Here are some common methods to perform **feature scaling**:

*   **Standardisation**
*   **Mean Normalisation**
*    **Min-Max Scaling**

* * *

Feature Selection & Feature Extraction
--------------------------------------

In practice, data often contains more information than is needed to build the model or the wrong kind of information. As the dimensionality of the data rises, the amount of data required to provide a reliable analysis grows exponentially. Bellman referred to this phenomenon as the “**curse of dimensionality**”.  
  
To overcome this problem it is necessary to find a way to reduce the number of features in consideration. Two techniques are often used:

*   **Feature Extraction:** Creating a subset of new features by combinations of the existing features.
*   **Feature Selection:** choosing a subset of all the features (the ones more informative).

*   ![](https://bhlin.co.network/wp/wp-content/uploads/2018/12/未命名-1-1024x265.png)
    

Usually**, feature extraction** is applied on the given data to extract features and **feature selection** is then applied with respect to the target variable to select the subset which can help in making a good model with good results.

* * *

*    Reference:

1.  [Python Machine Learning - Code Examples](http://nbviewer.jupyter.org/github/rasbt/python-machine-learning-book/blob/master/code/ch04/ch04.ipynb#Selecting-meaningful-features)
2.  [Training and Test Sets: Splitting Data](https://developers.google.com/machine-learning/crash-course/training-and-test-sets/splitting-data)[](https://medium.freecodecamp.org/understanding-gradient-descent-the-most-popular-ml-algorithm-a66c0d97307f)
3.  [5 Ways To Handle Missing Values In Machine Learning Datasets](https://www.analyticsindiamag.com/5-ways-handle-missing-values-machine-learning-datasets/)
4.  [How to Handle Missing Data with Python](https://machinelearningmastery.com/handle-missing-data-python/)
5.  [Why, How and When to Scale your Features](https://medium.com/greyatom/why-how-and-when-to-scale-your-features-4b30ab09db5e)
6.  [訓練集（train)、驗證集（validation）和測試集（test）的意義](https://hk.saowen.com/a/ccf871080e6f444ceba7924230f2cada409baa8a395900f8c677b365a33c1e4d)
7.  [Feature Selection and Feature Extraction in Machine Learning: An Overview](https://medium.com/@mehulved1503/feature-selection-and-feature-extraction-in-machine-learning-an-overview-57891c595e96)
8.  [机器学习中的特征——特征选择的方法以及注意点](https://blog.csdn.net/google19890102/article/details/40019271)