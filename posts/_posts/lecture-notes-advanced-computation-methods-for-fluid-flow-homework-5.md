---
title: '[Lecture Notes] Advanced Computation Methods for Fluid Flow – Homework 5'
tags:
  - Advanced Computation Methods for Fluid Flow - 2018
  - computational fluid dynamics
  - numerical method
id: '853'
date: 2018-05-24 12:47:15
---

> _23/05/2018, Homework No. 5_

* * *

Question
--------

Generate an algebraic grid for the solution domain shown in Figure 1 using the following database: **Edge 1:** straight line: \[latex\]x\_j= − 4 − 0.1( j − 1)\[/latex\], \[latex\]y\_j = 0\[/latex\], \[latex\]j = 1, 31 \[/latex\]. **Edge 2a:** circular segment: \[latex\]x\_j = − 3 − \\cos\\theta\_j \[/latex\], \[latex\]y\_j = \\sin\\theta\_j \[/latex\], \[latex\]θ\_j = 0.01( j − 1)\\pi \[/latex\], \[latex\]j = 1, 51 \[/latex\]. **Edge 2b:** straight line: \[latex\]x\_j = − 3 + 0.1( j − 1)\[/latex\], \[latex\]y\_j = 1\[/latex\], \[latex\]j = 1, 51 \[/latex\]. **Edge 2c:** elliptic segment: \[latex\]x\_j = 2 + 2 \\cos\\theta\_j \[/latex\], \[latex\]y\_j = \\sin\\theta\_j \[/latex\], \[latex\]θ\_j = 0.01(51 − j)\\pi \[/latex\], \[latex\]j = 1, 51 \[/latex\]. **Edge 2d:** straight line: \[latex\]x\_j = 4 + 0.1( j − 1)\[/latex\], \[latex\]y\_j = 0\[/latex\], \[latex\]j = 1, 51 \[/latex\]. **Edge 3:** straight line: \[latex\]x\_j = 9\[/latex\], \[latex\]y\_j = 0.2( j − 1)\[/latex\], \[latex\]j = 1, 21 \[/latex\]. **Edge 4a:** straight line: \[latex\]x\_j = −7\[/latex\], \[latex\]y\_j = 0.2( j − 1)\[/latex\], \[latex\]j = 1, 21 \[/latex\]. **Edge 4b, 4c, 4d & 4e:** straight line: \[latex\]x\_j = −7 + 0.2( j − 1)\[/latex\], \[latex\]y\_j = 4\[/latex\], \[latex\]j = 1, 81\[/latex\]. ![](https://bhlin.co.network/wp/wp-content/uploads/2018/05/擷取.png) Write a computer program to calculate the edge distributions for a 125×21 grid using the Vinokur functions (note: assume \[latex\]ds/d\\xi = \\Delta s\[/latex\] and omit iterations). Obtain the new edge-point distributions by linear interpolation of the database. **Edge 1:** \[latex\]\\Delta s\_1\[/latex\] = 0.01, \[latex\]\\Delta s\_2\[/latex\] = 0.40 (\[latex\]\\eta\[/latex\] = 1, 21) **Edge 2a:** \[latex\]\\Delta s\_1\[/latex\] = 0.02, \[latex\]\\Delta s\_2\[/latex\] = 0.10 (\[latex\]\\xi\[/latex\] = 1, 31) **Edge 2b:** \[latex\]\\Delta s\_1\[/latex\] = 0.10, \[latex\]\\Delta s\_2\[/latex\] = 0.10 (\[latex\]\\xi\[/latex\] = 31, 71) **Edge 2c:** \[latex\]\\Delta s\_1\[/latex\] = 0.10, \[latex\]\\Delta s\_2\[/latex\] = 0.04 (\[latex\]\\xi\[/latex\] = 71, 101) **Edge 2d:** \[latex\]\\Delta s\_1\[/latex\] = 0.05, \[latex\]\\Delta s\_2\[/latex\] = 0.50 (\[latex\]\\xi\[/latex\] = 101, 125) **Edge 3:** \[latex\]\\Delta s\_1\[/latex\] = 0.01, \[latex\]\\Delta s\_2\[/latex\] = 0.40 (\[latex\]\\eta\[/latex\] = 1, 21) **Edge 4a:** \[latex\]\\Delta s\_1\[/latex\] = 0.10, \[latex\]\\Delta s\_2\[/latex\] = 0.30 (\[latex\]\\xi\[/latex\] = 1, 16) **Edge 4b:** \[latex\]\\Delta s\_1\[/latex\] = 0.30, \[latex\]\\Delta s\_2\[/latex\] = 0.10 (\[latex\]\\xi\[/latex\] = 16, 31) **Edge 4c:** \[latex\]\\Delta s\_1\[/latex\] = 0.10, \[latex\]\\Delta s\_2\[/latex\] = 0.10 (\[latex\]\\xi\[/latex\] = 31, 71) **Edge 4d:** \[latex\]\\Delta s\_1\[/latex\] = 0.10, \[latex\]\\Delta s\_2\[/latex\] = 0.05 (\[latex\]\\xi\[/latex\] = 71, 101) **Edge 4e:** \[latex\]\\Delta s\_1\[/latex\] = 0.05, \[latex\]\\Delta s\_2\[/latex\] = 0.50 (\[latex\]\\xi\[/latex\] = 101, 125) Construct the two-dimensional grid using arclength-based transfinite interpolation (i.e. Soni TFI). Plot the numerical grids.

Answer
------

![](https://bhlin.co.network/wp/wp-content/uploads/2018/05/Figure_1-2.png)