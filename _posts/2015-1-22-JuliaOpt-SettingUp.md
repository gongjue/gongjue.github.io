---
layout: post
title: JuliaOpt Setting Up
---

## Jan 22

1. Download and Install Julia
2. Using Package Manager to install the following
  + `Cbc`
  + `Clp`
  + `GLPK`
  + `MathProgBase`
  + `GlpkMathProgBaseInterface` *(Error)*
  + `JuMP`
3. Package Manager command

  ```julia
  Pkg.add('Cbc') # add package named 'Cbc'
  Pkg.status()   # check installed packages
  Pkg.installed()
  Pkg.update()
  ```
4. Add JuliaOpt packages
  + `Convex`
  + `Optim`
  + `Gurobi`
5. Install IJulia

  ```julia
  Pkg.add("IJulia")
  ```




## Jan 23

1. Julia package dir: `~/.julia/v3.0/<pkg>`


## Jan 30

Examples from A Modeling Language for Mathematical Programming by R. Fourer, D.M. Gay and B.W. Kernighan:

+ a simple maximum-revenue production model
+ production and distribution planning
+ a static production model of a national fertilizer industry
+ multi-period production planning
+ allocation of cars to trains

Rewrite these 5 examples


