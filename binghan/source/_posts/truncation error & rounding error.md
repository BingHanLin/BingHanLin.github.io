---
title: Truncation error & Rounding error
tags:
  - numerical method
  - Uncategorized
id: '74'
date: 2018-03-20 00:08:00
mathjax: true
---

Introduction
------------

For many engineering problems, we cannot obtain analytical (true) solutions. That's why we employ numerical methods to obtain the solutions.  However, the numerical methods or algorithms are usually accompanied by computing with finite precision and errors of approximation (rounding and truncation). Before we get into the details of the topic, it is important to distinguish between accuracy and precision.
<!-- more -->

* **Accuracy**\- How close is a computed or measured value to the true value.
* **Precision** (or reproducibility) - How close is a computed or measured value to previously.

The figure below illustrates the difference between accuracy and precision.  The term error represents the imprecision and inaccuracy of a numerical computation.

![Alt text](https://od.lk/s/MTBfNDI3MTY1MjJf/Truncation%20Error%20%26%20Rounding%20Error_precision_accuracy.png) _(refer to http://www.antarcticglaciers.org/glacial-geology/dating-glacial-sediments-2/precision-and-accuracy-glacial-geology/)_

* * *

Truncation Error
----------------

**Definition** － The error is produced by an approximation in numerical approach to representing the actual value. Truncation errors are often seen in procedures of series (e.g. power series, Taylor series) and other algorithms where mathematical procedures get truncated (e.g. integration, limitation). Here we take Taylor series to explain the causes of truncation error. Let's consider the solution of  derivation of $f'_i=f'(x_i)$ for example. Using Taylor expansion to approximate $f_{i+1}=f'(x_{i+1})$ about $f_i=f(x_i) $ :

$$
\eqalign{f_{i+1}=f_i+hf'_i+\frac{h^2}{2}f^{\prime\prime}_i+\frac{h^3}{6}f^{\prime\prime\prime}_i+\frac{h^4}{24}f^{\prime\prime\prime\prime}_i+...}
$$

Replace the $f'_i$ term into left side, we can obtained,

$$
\eqalign{ f' = \frac{f_{i+1}-f_i}{h}-\frac{h}{2}f^{\prime\prime}_i-\frac{h^2}{6}f^{\prime\prime\prime}_i-\frac{h^3}{24}f^{\prime\prime\prime\prime}_i+... = \frac{f_{i+1}-f_i}{h} +E}$$

where $ h$ is a small step size,  $ E$ the truncation error. With a leading term $ - (h/2)f^{\prime\prime}_i$ , the truncation error become $ E\cong- (h/2)f^{\prime\prime}_i + O(h^2)$ where the remaining terms in  $ O(h^2)$ can be neglected due to their small value. Since the dominating term of $ E$  is proportional to $ h$,  we say that the truncation error is of first order in $ h$. The first terms on the right side is also one of the form for forward difference scheme.  Similarly, error can also be estimate for backward difference approximation and central difference approximation.

* * *

Rounding Errors
---------------

**Definition** －The error produced by computer limited significant figures to represent the actual result. Because floating-point numbers have a limited number of digits, they cannot represent all real numbers accurately. When there are more digits than the format allows, the leftover ones are omitted (the number is rounded), and this cause errors. Some examples are list in the following table:

![Alt text](https://bhlin.co.network/wp/wp-content/uploads/2018/03/未命名.png)
*refer to [wikipedia](https://en.wikipedia.org/wiki/Round-off_error)*

* * *

Total Errors
------------

Total errors in computational simulation(neglect other factors e.g.  artificial error, wrong data)  equal to the sum of truncation errors  and rounding errors. In order to eliminate the total error , the minimum value of truncation error and rounding error are needed.  Unfortunately , it is not possible to select a step size that keep both  to minimum because they have a relationship as following figure.

![Alt text](https://bhlin.co.network/wp/wp-content/uploads/2018/03/img60.png) 
*refer to [link](https://me.ucsb.edu/~moehlis/APC591/tutorials/tutorial5/node3.html)*

But we can choose to use ideal step size to achieve the minimum total errors. The process usually starts from (a) Select a step size $h $, compute solution;  (b) Use $h/2 $, re-compute; (c) If new result closes to the previous, the $h $ is probably acceptable. If not, then reduce $h $ again.

* * *

*   Reference:

1.  [Truncation Error Analysis](http://hplgit.github.io/INF5620/doc/pub/main_trunc-2up.pdf)
2.  [Truncation versus rounding](http://www.cs.cornell.edu/~bindel/class/cs3220-s12/notes/lec22.pdf)
3.  [Round-off error](https://en.wikipedia.org/wiki/Round-off_error)