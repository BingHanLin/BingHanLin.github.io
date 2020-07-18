---
title: Introduce to ANSYS Workbench Scripting - Part 2
tags:
  - Computational Fluid Dynamics (CFD)
id: '1609'
date: 2019-03-15 00:28:30
---

With the knowledge in previous [article](https://bhlin.co.network/wp/2019/01/20/introduce-to-ansys-workbench-scripting-part-1/), we will show how to write and execute a Python script in ANSYS Workbench by a simple example.

What does this script do?
-------------------------

**Imagine this scenario:** You have performed a set of analyses on a design with an initial geometry file. These analyses have been saved as a number of different ANSYS Workbench projects. Now, you are asked for replacing the initial geometry configuration with the new one and update these analyses.

Then you would like to write a script help you complete the task on all affected projects automatically. The script would do the following:

1.  Create a new directory for saving the new design analyses projects later.
2.  Finds all ANSYS Workbench projects within a specified directory.
3.  For each project that has been found:
    *   Replaces the original geometry with the new geometry file in all system in the project.
    *   Updates the project and save customize information to a log file.
    *   Saves the modified project to a new directory.

![](https://bhlin.co.network/wp/wp-content/uploads/2019/03/圖片1-300x244.png)

Directory tree of the working folder.

We first prepare the working folder contain a python script, new geometry file, and a set of original ANSYS Workbench projects.

* * *

Write the script
----------------

*   Import packages that we need later.

import os
import clr
clr.AddReference("Microsoft.Office.Interop.Excel")
import Microsoft.Office.Interop.Excel as Excel

*   Get the current directory (where python script exist), and set current directory path as user path. Define the directory path of the original project and the modified project.

currentDirectory = os.getcwd()
SetUserPathRoot(DirectoryPath = currentDirectory)

origDir = AbsUserPathName("Original")
newDir = AbsUserPathName("Modified")

*   Get the path of new geometry file.

newGeom = AbsUserPathName("newGeom.agdb")

*   Create the new directory and the log file.

\# Create the new directory if necessary
if not os.path.exists(newDir):        
    os.makedirs(newDir)

# Create the log file in new directory
logFile = open( newDir+"\\ MyScript.log ","w")

*   Save the Workbench project in the original directory and save them to a list.

projFile\_list = \[\]
# Find projects in the original directory    
for fileName in os.listdir(origDir):
    if fileName.endswith(".wbpj"):
        projFile\_list.append(fileName)

*   Loop through all the projects. For each project in the list:
    1.  Replaces the original geometry with the new geometry file.
    2.  Updates the project and save reports in log file.
    3.  Saves the modified project with the new geometry file to a new directory.

for projFile in projFile\_list:
    # Open the project into Workbench and clear any starting messages
    origProjPath = os.path.join(origDir, projFile)
    newProjPath = os.path.join(newDir, projFile)

    Open(FilePath = origProjPath)
    ClearMessages()
    logFile.write("Processing project in " + origProjPath + "\\n")

    for system in GetAllSystems():
        logFile.write("Find system - " + system.DisplayText + "\\n")
        try:
            geometry = system.GetContainer(ComponentName="Geometry")
        except:
            logFile.write("No geometry to replace in system - " + system.DisplayText + "\\n")
        else:
            geometry.SetFile(FilePath=newGeom)
            logFile.write("Replace geometry in system - " + system.DisplayText + "\\n")
        
        # Update the project
        Update()
        logFile.write("Update system - " + system.DisplayText + "\\n")

    Save(FilePath = newProjPath, Overwrite=True)
    logFile.write("Save project in " + newProjPath + "\\n")

logFile.close()

The whole script becomes:

import os
import clr
clr.AddReference("Microsoft.Office.Interop.Excel")
import Microsoft.Office.Interop.Excel as Excel

# Set current directory path as user path
currentDirectory = os.getcwd()
SetUserPathRoot(DirectoryPath = currentDirectory)

origDir = AbsUserPathName("Original")
newDir = AbsUserPathName("Modified")
newGeom = AbsUserPathName("newGeom.agdb")

# Create the new directory if necessary
if not os.path.exists(newDir):        
    os.makedirs(newDir)

# Create the log file in new directory
logFile = open( newDir+"\\ MyScript.log ","w")

projFile\_list = \[\]
# Find projects in the original directory    
for fileName in os.listdir(origDir):
    if fileName.endswith(".wbpj"):
        projFile\_list.append(fileName)

for projFile in projFile\_list:
    # Open the project into Workbench and clear any starting messages
    origProjPath = os.path.join(origDir, projFile)
    newProjPath = os.path.join(newDir, projFile)

    Open(FilePath = origProjPath)
    ClearMessages()
    logFile.write("Processing project in " + origProjPath + "\\n")

    for system in GetAllSystems():
        logFile.write("Find system - " + system.DisplayText + "\\n")
        try:
            geometry = system.GetContainer(ComponentName="Geometry")
        except:
            logFile.write("No geometry to replace in system - " + system.DisplayText + "\\n")
        else:
            geometry.SetFile(FilePath=newGeom)
            logFile.write("Replace geometry in system - " + system.DisplayText + "\\n")
        
        # Update the project
        Update()
        logFile.write("Update system - " + system.DisplayText + "\\n")

    Save(FilePath = newProjPath, Overwrite=True)
    logFile.write("Save project in " + newProjPath + "\\n")

logFile.close()

* * *

Run the script
--------------

Before running the python script above, let's add the path of ANSYS Workbench into environment variables. Check this [website](https://www.architectryan.com/2018/03/17/add-to-the-path-on-windows-10/) to see how to add environment variables on Windows10. The path of ANSYS Workbench should be like:  

    <installation path>/<version>/Framework/bin/<platform>/runwb2

Now, we can replay the specified ANSYS Workbench script file on start-up by executing the following command in Command Prompt.

    runwb2 -r my_script.py

Note: the command should be executed in the directory where the python script exists.

After executing the script, we will get a directory contains a set of new analysis results.

This simple example can be extend to

![](https://bhlin.co.network/wp/wp-content/uploads/2019/03/圖片2-261x300.png)

Directory tree of the working folder after executing the script.

This simple example can be extended to more complex manipulations which introduce additional computations in scripts or interact with other applications such as Excel.