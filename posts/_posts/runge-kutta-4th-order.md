---
title: Runge Kutta 4th Order
tags:
  - numerical method
  - python
  - Uncategorized
id: '103'
date: 2018-03-19 22:49:27
---

Introduction
------------

Runge-Kutta method is a numerical procedure for approximating values for the solution of ordinary differential equations (ODEs) with a given initial value. The simplest Runge–Kutta method has the same form as Euler method.

* * *

Problem Statement
-----------------

Let's consider an IVP (Initial Value Problem)  as follow,

\[latex\]\\eqalign{{{dy(t)} \\over {dt}} = y'(t) = f(y(t),t), \\quad \\quad {\\rm{with\\;}} y(t\_0)=y\_0 }\[/latex\]

The value of \[latex\]y(t)\[/latex\] is the solution we want to obtain. Here, the derivative of our solution at time \[latex\]t\[/latex\], \[latex\]y(t)\[/latex\], is dependent on that solution and \[latex\]t\[/latex\]. The approximate techniques are described and implement by Python code below.

* * *

First Order Runge-Kutta (Euler's Method)
----------------------------------------

Using the Taylor Series to expand \[latex\]y(t)\[/latex\] at \[latex\] t=0\[/latex\].

\[latex\]y(t) = y(0) + y'(0)t + y''(0){{{t^2}} \\over 2} + \\cdots\[/latex\]

Then we approximate the solution in a short step, \[latex\] h\[/latex\], after \[latex\] t=0\[/latex\] and truncate the Taylor series after the first derivative.

\[latex\]\\eqalign{ & y(h) = y(0) + y'(0)h + y''(0){{{h^2}} \\over 2} + \\cdots \\cr & y(h) \\approx y(0) + y'(0)h \\cr}\[/latex\]

Now, we have obtained the solution at \[latex\] t=h\[/latex\] with the error in \[latex\] O({h^2})\[/latex\] . Take the same concept into every steps afterward, the general formula for the fist order runge-kutta method is given as,

\[latex\]y\_{n+1} \\approx y\_n +h f(y\_n,{t\_n}) \[/latex\]

where the subscript \[latex\]n\[/latex\] denotes the number of  steps, \[latex\]h\[/latex\] denotes a small step size. It advances the solution through an interval \[latex\]h\[/latex\] by using the derivatives information at the beginning of that interval. We can use Python code with a simple loop to complte the procedure above. \[python\] # Solve y'(t)=-2y(t)+cos(4t) with y0=3 import math import matplotlib.pyplot as plt import numpy as np y0 = 3 # Initial Condition h = 0.1 # Time step t = np.arange( 0, 2+h, h ); # Calculate from 0 to 2 seconds # Exact solution, hard to find in this case (in general we won't have it) yexact = 0.1\*np.cos(4\*t)+0.2\*np.sin(4\*t)+2.9\*np.exp(-2\*t) ystar = np.zeros(t.size); # Preallocate array (good coding practice) ystar\[0\] = y0; # Initial condition gives solution at t=0 # Start of the loop for i in range(0,t.size-1): k1 = -2\*ystar\[i\]+np.cos(4\*t\[i\]); # Deriv information from previous state ystar\[i+1\] = ystar\[i\] + k1\*h; # Calculate solution for next value of y # End of the loop # Plot the result line1, = plt.plot(t,yexact,'r', label='Exact solution') line2, = plt.plot(t, ystar, 'bo--', label=('Numerical solution, h = '+str(h))) plt.legend(handles = \[line1, line2\]) plt.title('Exact and Numerical Solution') plt.xlabel('time (t)') plt.ylabel('Solution of y(t)') plt.show() print ('Complete!') \[/python\] A figure of the result is shown here. One thing to be noticed is that the accuracy of the numerical solution can be improved by reducing the step size \[latex\]h\[/latex\].

![Alt text](http://i58.photobucket.com/albums/g269/jaguar3096/reunge%20kutta_zpsu0ls1q4t.png)

* * *

Fourth Order Runge-Kutta
------------------------

First order Runge-Kutta (Euler's method) is not recommended for practical use due to its low accuracy and stability. One way we could improve the solutions based on the similar concept above. We again calculate the slope at the beginning point, and instead of forwarding to next step, we take a "trail" step to the midpoint of the interval. Then compute the slope at the midpoint. Finally, use this slope to cross the whole interval from the beginning point. The equations of this idea are presented as follow,

\[latex\]k\_1 = hf({y\_n,t\_n})\[/latex\]

\[latex\]k\_2 = hf({y\_n+\\frac{1}{2}k\_1,t\_n+\\frac{1}{2}h})\[/latex\]

\[latex\]y\_{n+1} =y\_n+k\_2+O(h^3) \[/latex\]

In fact, it is called the second-order Runge-Kutta method. But, we don't stop here.  By continuing taking more "trail" steps in an interval, a higher order algorithm can be expected. The classical fourth-order Runge-Kutta method is derived as,

\[latex\]k\_1 = hf({y\_n,t\_n}) \[/latex\]

\[latex\]k\_2 = hf({y\_n+\\frac{1}{2}k\_1,t\_n+\\frac{1}{2}h})\[/latex\]

\[latex\]k\_3 = hf({y\_n+\\frac{1}{2}k\_2,t\_n+\\frac{1}{2}h})\[/latex\]

\[latex\]k\_3 = hf({y\_n+k\_3,t\_n+h})\[/latex\]

\[latex\]y\_{n+1} =y\_n+\\frac{k\_1}{6}+\\frac{k\_2}{3}+\\frac{k\_3}{3}+\\frac{k\_4}{6}+O(h^5) \[/latex\]

We can repeat this process using this estimate by a loop over the whole duration. \[python\] # Solve y'(t)=-2y(t)+cos(4t) with y0=3, 4th order Runge Kutta import math import matplotlib.pyplot as plt import numpy as np y0 = 3 # Initial Condition h = 0.1 # Time step size t = np.arange( 0, 2+h, h ) # Calculate from 0 to 2 seconds # Exact solution, hard to find in this case (in general we won't have it) yexact = 0.1\*np.cos(4\*t)+0.2\*np.sin(4\*t)+2.9\*np.exp(-2\*t) ystar = np.zeros(t.size) # Preallocate array (good coding practice) ystar\[0\] = y0 # Initial condition gives solution at t=0 # Start of the loop for i in range(0,t.size-1): k1 = -2\*ystar\[i\] + np.cos(4\*t\[i\]) y1 = ystar\[i\] + k1\*h/2 k2 = -2\*y1 + np.cos(4\*t\[i\] + k1\*h/2) y2 = ystar\[i\] + k2\*h/2 k3 = -2\*y2 + np.cos(4\*t\[i\] + k2\*h/2) y3 = ystar\[i\] + k3\*h/2 k4 = -2\*y3 + np.cos(4\*t\[i\] + k3\*h/2) ystar\[i+1\] = ystar\[i\] + (k1+2\*k2+2\*k3+k4)\*h/6 # Calculate solution for next value of y # End of the loop # Plot the result line1, = plt.plot(t,yexact,'r', label='Exact solution') line2, = plt.plot(t, ystar, 'bo--', label=('Numerical solution, h = '+str(h))) plt.legend(handles = \[line1, line2\]) plt.title('Exact and Numerical Solution') plt.xlabel('time (t)') plt.ylabel('Solution of y(t)') plt.show() print ('Complete!') \[/python\] The fourth-order Runge-Kutta method required four slopes per step \[latex\]h\[/latex\]. Will that produce superior accuracy to the first order method? If we see in the figure ( the result of 4th RK) below, the answer seems to be "yes".  But it more often depends on the nature of the problems we try to solve.

![Alt text](http://i58.photobucket.com/albums/g269/jaguar3096/reunge%20kutta4th_zpsvxtavvpy.png)

* * *

*   Reference:

1.  [Approximation of Differential Equations by Numerical Integration](http://lpsa.swarthmore.edu/NumInt/NumIntIntro.html)
2.  [常微分程求解：隆巨—庫塔法、高階方法的圖像](http://boson4.phys.tku.edu.tw/numerical_methods/nm_units/ODE_Runge-Kutta.htm)
3.  THE ART OF SCIENTIFIC COMPUTING (ISBN 0-521-43108-5), 1988-1992 by Cambridge University Press