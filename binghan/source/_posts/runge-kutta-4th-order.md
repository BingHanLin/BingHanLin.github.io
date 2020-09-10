---
title: Runge Kutta 4th Order
tags:
  - Numerical Method
  - Python
categories: 
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

