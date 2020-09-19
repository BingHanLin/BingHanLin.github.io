---
title: Runge Kutta 4th Order
tags:
  - Numerical Method
  - Python
categories: 
  - Uncategorized
id: '103'
date: 2018-03-19 22:49:27
mathjax: true
---

Introduction
------------

Runge-Kutta method is a numerical procedure for approximating values for the solution of ordinary differential equations (ODEs) with a given initial value. The simplest Runge–Kutta method has the same form as Euler method.
<!-- more -->
* * *

Problem Statement
-----------------

Let's consider an IVP (Initial Value Problem)  as follow,

$$
\eqalign{\frac{dy(t)}{dt} = y'(t) = f(y(t),t), \quad \rm{with}\quad y(t_0)=y_0}
$$

The value of $y(t)$ is the solution we want to obtain. Here, the derivative of our solution at time $t$, $y(t)$, is dependent on that solution and $t$. The approximate techniques are described and implement by Python code below.

* * *

First Order Runge-Kutta (Euler's Method)
----------------------------------------

Using the **Taylor Series** to expand $y(t)$ at $ t=0$.

$$
\eqalign{y(t) = y(0) + y'(0)\frac{t} {1}+ y''(0)\frac{t^2} {2} + \cdots}
$$

Then we approximate the solution in a short step, $h$, after $t=0$ and truncate the Taylor series after the first derivative.

$$
\eqalign{ & y(h) = y(0) + y'(0)h + y''(0)\frac{h^2}{2} + \cdots \cr & y(h) \approx y(0) + y'(0)h \cr}
$$

Now, we have obtained the solution at $t=h$ with the error in $O({h^2})$ . Take the same concept into every steps afterward, the general formula for the fist order runge-kutta method is given as,

$$
\eqalign{y_{n+1} \approx y_n +h f(y_n,{t_n})}
$$

where the subscript $n$ denotes the number of  steps, $h$ denotes a small step size. It advances the solution through an interval $h$ by using the derivatives information at the beginning of that interval. We can use Python code with a simple loop to complte the procedure above.

```python
# Solve y'(t)=-2y(t)+cos(4t) with y0=3
 
import math
import matplotlib.pyplot as plt
import numpy as np
 
y0 = 3 # Initial Condition
h = 0.1 # Time step
t = np.arange( 0, 2+h, h ); # Calculate from 0 to 2 seconds
 
# Exact solution, hard to find in this case (in general we won't have it)
yexact = 0.1*np.cos(4*t)+0.2*np.sin(4*t)+2.9*np.exp(-2*t)
ystar = np.zeros(t.size); # Preallocate array (good coding practice)
 
ystar[0] = y0; # Initial condition gives solution at t=0
 
# Start of the loop
for i in range(0,t.size-1):
    k1 = -2*ystar[i]+np.cos(4*t[i]); # Deriv information from previous state
    ystar[i+1] = ystar[i] + k1*h; # Calculate solution for next value of y
# End of the loop
 
# Plot the result
line1, = plt.plot(t,yexact,'r', label='Exact solution')
line2, = plt.plot(t, ystar, 'bo--', label=('Numerical solution, h = '+str(h)))
 
plt.legend(handles = [line1, line2])
plt.title('Exact and Numerical Solution')
plt.xlabel('time (t)')
plt.ylabel('Solution of y(t)')
 
plt.show()
 
print ('Complete!')
```

A figure of the result is shown here. One thing to be noticed is that the accuracy of the numerical solution can be improved by reducing the step size $h$.

![](https://i.imgur.com/wu9stb8.png)

* * *

Fourth Order Runge-Kutta
------------------------

First order Runge-Kutta (Euler's method) is not recommended for practical use due to its low accuracy and stability. One way we could improve the solutions based on the similar concept above. We again calculate the slope at the beginning point, and instead of forwarding to next step, we take a "trail" step to the midpoint of the interval. Then compute the slope at the midpoint. Finally, use this slope to cross the whole interval from the beginning point. The equations of this idea are presented as follow,

$$
\eqalign{y_{n+1} \approx y_n +h f(y_n,{t_n})}
$$

$$
\eqalign{k_1 = hf({y_n,t_n})}
$$

$$
\eqalign{k_2 = hf({y_n+\frac{1}{2}k_1,t_n+\frac{1}{2}h})}
$$

$$
\eqalign{y_{n+1} =y_n+k_2+O(h^3) }
$$

In fact, it is called the second-order Runge-Kutta method. But, we don't stop here.  By continuing taking more "trail" steps in an interval, a higher order algorithm can be expected. The classical fourth-order Runge-Kutta method is derived as,


$$
\eqalign{k_1 = hf({y_n,t_n})}
$$

$$
\eqalign{k_2 = hf({y_n+\frac{1}{2}k_1,t_n+\frac{1}{2}h})}
$$

$$
\eqalign{k_3 = hf({y_n+\frac{1}{2}k_2,t_n+\frac{1}{2}h})}
$$

$$
\eqalign{k_3 = hf({y_n+k_3,t_n+h})}
$$

$$
\eqalign{y_{n+1} =y_n+\frac{k_1}{6}+\frac{k_2}{3}+\frac{k_3}{3}+\frac{k_4}{6}+O(h^5)}
$$

We can repeat this process using this estimate by a loop over the whole duration.


```python
# Solve y'(t)=-2y(t)+cos(4t) with y0=3, 4th order Runge Kutta
 
import math
import matplotlib.pyplot as plt
import numpy as np
 
y0 = 3                  # Initial Condition
h = 0.1                 # Time step size
t = np.arange( 0, 2+h, h )   # Calculate from 0 to 2 seconds
 
# Exact solution, hard to find in this case (in general we won't have it)
yexact = 0.1*np.cos(4*t)+0.2*np.sin(4*t)+2.9*np.exp(-2*t)
ystar = np.zeros(t.size)   # Preallocate array (good coding practice)
 
ystar[0] = y0              # Initial condition gives solution at t=0
 
 
# Start of the loop
for i in range(0,t.size-1):
 
    k1 = -2*ystar[i] + np.cos(4*t[i])    
    y1 = ystar[i] + k1*h/2
 
    k2 = -2*y1 + np.cos(4*t[i] + k1*h/2)
    y2 = ystar[i] + k2*h/2
 
    k3 = -2*y2 + np.cos(4*t[i] + k2*h/2)
    y3 = ystar[i] + k3*h/2
 
    k4 = -2*y3 + np.cos(4*t[i] + k3*h/2)  
    ystar[i+1] = ystar[i] + (k1+2*k2+2*k3+k4)*h/6       # Calculate solution for next value of y
# End of the loop
 
# Plot the result
line1, = plt.plot(t,yexact,'r', label='Exact solution')
line2, = plt.plot(t, ystar, 'bo--', label=('Numerical solution, h = '+str(h)))
 
plt.legend(handles = [line1, line2])
plt.title('Exact and Numerical Solution')
plt.xlabel('time (t)')
plt.ylabel('Solution of y(t)')
 
plt.show()
 
print ('Complete!')
```

The fourth-order Runge-Kutta method required four slopes per step $h$. Will that produce superior accuracy to the first order method? If we see in the figure ( the result of 4th RK) below, the answer seems to be "yes". But it more often depends on the nature of the problems we try to solve.

![](https://i.imgur.com/60YRGzo.png)

* * *

*   Reference:

1.  [Approximation of Differential Equations by Numerical Integration](http://lpsa.swarthmore.edu/NumInt/NumIntIntro.html)
2.  [常微分程求解：隆巨—庫塔法、高階方法的圖像](http://boson4.phys.tku.edu.tw/numerical_methods/nm_units/ODE_Runge-Kutta.htm)
3.  THE ART OF SCIENTIFIC COMPUTING (ISBN 0-521-43108-5), 1988-1992 by Cambridge University Press
