---
title: Driving ANSYS Workbench and Excel through a Python script
tags:
  - Uncategorized
id: '1367'
---

I have recently been working on a task which needs to establish a customized procedure for **ANSYS Workbench**. And it would be better if an **Excel** file can be created to record all the data during the simulation. Fortunately, **Python language** works well with Excel and Workbench, we are able to use it to connect the two. 

**ANSYS Workbench** and **Python**
----------------------------------

Here are the important points for connecting **ANSYS Workbench** and **Python language**:

*   Workbench has IronPython built into it from the ground up.
*   You can record whatever you do in the GUI to create scripts.
*   You can read those scripts in to control Workbench.
*   ANSYS uses IronPython because it talks to Windows programs.

> http://www.padtinc.com/blog/the-focus/workbench-scripting-using-forms-in-your-script http://www.padtinc.com/blog/the-focus/workbench-and-excel-part-2-driving-workbench-from-excel-with-python

[Workbench and Excel, Part 2: Driving Workbench From Excel with Python – PADT, Inc. – The Blog](http://www.padtinc.com/blog/the-focus/workbench-and-excel-part-2-driving-workbench-from-excel-with-python)

[Workbench Scripting: Using Forms in your Script – PADT, Inc. – The Blog](http://www.padtinc.com/blog/the-focus/workbench-scripting-using-forms-in-your-script)

[Starting ANSYS Products From the Command Line – PADT, Inc. – The Blog](http://www.padtinc.com/blog/the-focus/starting-ansys-products-from-the-command-line)