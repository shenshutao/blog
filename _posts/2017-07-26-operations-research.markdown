---
layout: splash
title: "Operations Research"
date:   2017-07-26 19:06:46 +0800
categories: machine learning
comments: false
share: true
publish: true
---

# Brief
The application of scientific methods to the study of operations of large complex organizations or activities in order to give executives a quantitative basis for reaching optimum decisions

# Sample Questions (Applications)
Reddy Mikks produces both interior and exterior paints from two raw materials, M1 and M2. The following table provides the basic data of the problem:

![image01]({{ site.baseurl }}/img/img01.png){:width="500px"} 

__How to achieve the maximum profit ?__

# Steps:
1. Problem Definition and Data Gathering
2. __Mathematical Model Building__ (introduce below)
3. Developing Solution Approach
5. Model Solution Testing 
6. Implementation

__Finding Jobs'__
- Decision variable: _No. of M1, x1 and No. of M2, x2_
- Objective: _Maximum profit_
- Constraint: _Limitation of the materials_

__Mathematic descriptiong__
- Decision variable: 
>* X1 = Tons produced daily of exterior paint
>* X2 = Tons produced daily of interior paint
- Objective function: _Maximize the total daily profit (z) 
>* z=5\*X1 + 4\*X2
- Constraint: 
>* 6\*X1 + 4\*X2 ≤ 24 ( Raw material M1)
>* X1 + 2\*X2 ≤ 6 (RawmaterialM2)

# Methods
1. Graphical Solution Method ( for 2 decision variables problem, we can draw a graphy and slove it. )
2. __Simplex Method__ ( a general solution technique for solving LP problem. introduce below. )

# Simplex Method
## Definition
- __Extreme point solution (corner point solution):__ 
 Solution points that lie on the intersection of a number of constraint lines.
- __Adjacent Extreme point solution:__
 Two extreme point solutions are adjacent extreme points if they are connected by a constraint line (2-dimension case).
- An optimal solution is always a __corner point__ solution and none of the adjacent extreme point solution is better off in the value of the objective function.



