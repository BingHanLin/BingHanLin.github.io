---
title: Introduce to ANSYS Workbench Scripting - Part 1
tags:
  - Computational Fluid Dynamics (CFD)
id: '1597'
date: 2019-01-20 01:34:06
---

Journaling
----------

A journal is a record of all operations that have **modified project data** during your session. We can **record** a journal and then to **playback** a journal which performs the previously recorded actions again.

Journals are recorded as **Python-based scripts**. The **command window** in ANSYS Workbench allows user to invoke commands, access data entity properties, and invoke data entity and data container methods interactively, one at a time.

ImportJournalVariables()?

* * *

Scripting
---------

A script is a set of commands to be sent to ANSYS Workbench. The script can be a **modified journal**, or it can be a completely new set of commands that user write directly. As mentioned above, scripting is based on **IronPython** which is well integrated with the .NET Framework.

* * *

Scripting and Data-Integrated Applications
------------------------------------------

Users can interact with applications that are **native to ANSYS Workbench** (called workspaces), and you can launch applications that are **data-integrated**. The difference between native workspaces and data-integrated applications is an important consideration for ANSYS Workbench journaling and scripting.

### **Native Workspaces**

All operations that modify the data associated with a native workspace are journaled and can be fully automated with ANSYS Workbench scripting.  
( Project Schematic, Engineering Data, and Design Exploration... )

### **Data-Integrated Applications**

Operations performed within the data-integrated application are not necessarily journaled or controlled by ANSYS Workbench scripting. ( Mechanical APDL application, ANSYS Fluent, ANSYS CFX, DesignModeler, and the Mechanical application... )

Although data-integrated applications do not fully support ANSYS Workbench scripting, many of them have **their own native scripting language** which is accessible through the ANSYS Workbench scripting interface. Users can insert _SendCommand_ calls into your ANSYS Workbench scripts to drive data-integrated applications.

The table below lists scripting supports for each data-Integrated applications.

**Data-Integrated Applications**

**Native Scripting Language**

**Supports Scripting with Send Command**

Mechanical APDL

APDL

Yes

Mechanical

JScript

Yes

CFX

CCL

Yes

Fluent

Scheme

Yes

Aqwa

JScript

Yes

CFD-Post

CCL

Yes

FE Modeler

JScript

Yes

DesignModeler

JScript

Yes

Meshing

JScript

Yes

ICEM CFD

TCL

Yes

* * *

ANSYS Workbench Project and Data Model Concepts
-----------------------------------------------

### Project Elements

![](https://bhlin.co.network/wp/wp-content/uploads/2019/01/圖片1-1024x686.png)

Project and Data Model Concepts

#### Project

The project is the full collection of systems, components, data, and their connections.

#### System

A system is **a collection of components** that together provide **workflow** to achieve an engineering simulation goal. Systems may also contain a single component to complete an analysis sub-task.

#### Component

A component includes a collection of **data** and a **data editor** that work together to achieve a CAE-related task. A data editor can be an ANSYS Workbench-enabled application or a native ANSYS Workbench workspace.

#### Data Container

A data container includes data unique to an individual component as well as the services to manage and manipulate it.

#### Data Entity

A data entity is a data structure defined within the data container. A data container often employs several data entities. A data entity is similar to a class in an object-oriented programming language; **it defines member data (or properties) and methods** which can be called to perform operations on the data.

#### Data Reference, Data Container Reference

A handle to an instantiated data entity and instantiated data container object.

### Template

ANSYS Workbench uses templates to **create the Projects, System, and Components elements described above**. A template is a high-level description of the item to be created, but does not contain specific detailed data.