---
title: "相关系数 - Correlation coefficient"
date: 2017-11-04 10:00:00 +0800
categories:
- data
tags:
- 相关系数
layout: splash
comments: false
share: false
published: false
---
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
# 相关系数

## 简介
相关系数是研究变量之间线性相关程度的量。相关系数越接近1，说明两个变量之间的正相关性越强，即一个变量上升的时候，另外一个变量也在上升，帮助我们在构建线性模型时选择自变量X。

## 数学公式
### 相关系数
$$ r(X,Y)=\frac{Cov(X,Y)}{\sqrt{Var[X]Var[Y]}} $$

其中 Cov(X,Y) 为X与Y的协方差，Var[X]为X的方差，Var[Y]为Y的方差

### 协方差
协方差（Covariance）在概率论和统计学中用于衡量两个变量的总体误差。
Cov(X，Y)=E(XY)-E(X)E(Y)

其中 E(XY)是X*Y的期望值, E(X)是X的期望值, E(Y)是Y的期望值

### 期望值
如果X是在概率空间（Ω, P）中的随机变量，那么它的期望值E[X]的定义是：
$$ E(X) = \int_{\Omega }^{ } X dF $$

### 概率空间
