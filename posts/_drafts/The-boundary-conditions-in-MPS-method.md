---
title: The boundary conditions in MPS method
tags:
  - Uncategorized
id: '2239'
---

Introduction
------------

In the Moving Particle Semi-implicit (MPS) method, the spatial derivatives of the physical quantities (e.g., velocity and pressure) and value of the particle number density are calculated by referencing the relative positions of surrounding particles that present inside the effective domain, but **for particles located near boundary, the effective domain is truncated by the boundary**.

Therefore, an additional boundary treatment is necessary not only for the implementation of the physical boundary condition but also for proper management of the near-boundary particle distribution and preventing particles from unphysical behaviors.

Boundaries that appear in fluid flow simulations using the Moving Particle Semi-implicit (MPS) method can mostly be classified into four types: **(1) solid wall, (2) free surface, (3) inlet/outlet boundary, and (4) periodic boundary**.

Solid Wall
----------

For the solid wall boundaries, the appropriate boundary representations need to achieve two important tasks: **(1) enforcement of physical boundary condition, (2) compensation of particle deficiency**.

In most MPS simulations the solid wall boundaries can be represented using either particles or polygons. For both of them, we can express the discretization schemes and the particle number density in a general form:

### Particle Representation: Wall Particle

### Particle Representation: Mirror Particle

### Polygon Representation: Distance Function - Based

### Polygon Representation: Boundary Integral - Based

Free Surface
------------