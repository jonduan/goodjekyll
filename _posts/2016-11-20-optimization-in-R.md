---
published: true
layout: post
title: Optimization in R
category: optimization
tags:
  - optimization
  - R
  - Julia
  - GAMS
---
Last month, I taught a lab about how to do optimization in R using ROI.

I also would likt to introduce JUMP in Julia which is taught in MIT optimization course.

I am surprised that [OMPR](https://github.com/dirkschumacher/ompr) acctually combinds ROI and JUMP.

> OMPR (Optimization Modelling Package) is a DSL to model and solve Mixed Integer Linear Programs. It is inspired by the excellent Jump project in Julia.


## One simple example is 

```r
library(dplyr)
library(ROI)
library(ROI.plugin.glpk)
library(ompr)
library(ompr.roi)

result <- MIPModel() %>%
  add_variable(x, type = "integer") %>%
  add_variable(y, type = "continuous", lb = 0) %>%
  set_bounds(x, lb = 0) %>%
  set_objective(x + y, "max") %>%
  add_constraint(x + y <= 11.25) %>%
  solve_model(with_ROI(solver = "glpk")) 
get_solution(result, x)
get_solution(result, y)
```


## Funtions

 - MIPModel() create an empty mixed integer linear model

 - add_variable() adds variables to a model

 - set_objective() sets the objective function of a model

 - set_bounds()sets bounds of variables

 - add_constraint() add constraints

 - solve_model() solves a model with a given solver

 - get_solution() returns the solution of a solved model for a given variable or group of variables


## Solver

Solvers are in different packages. ompr.ROI uses the ROI package which offers support for all kinds of solvers.

 - with_ROI(solver = "glpk") solve the model with GLPK. Install ROI.plugin.glpk
 
 - with_ROI(solver = "symphony") solve the model with Symphony. Install ROI.plugin.symphony
 
 - with_ROI(solver = "cplex") solve the model with CPLEX. Install ROI.plugin.cplex
 
 - ... See the ROI package for more plugins.


## Source

And I knew this from a great blog [Yet Another Math Programming Consultant](http://yetanothermathprogrammingconsultant.blogspot.ca/search?updated-max=2016-09-07T12:43:00-04:00&max-results=10&start=26&by-date=false) in Amsterdam. 

[Erwin Kalvelagen](https://plus.google.com/100547539949080099832) practices optimization in R, GAMS, and Julia. 

It is worth reading his blog.

[gdxrrw and R 3.3.1](gdxrrw and R 3.3.1)

I will definitely try this approach to integrate R and GAMS these two great tools.


