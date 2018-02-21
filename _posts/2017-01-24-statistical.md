---
layout: splash
title: "Applied Engineering Statistics"
date:   2017-09-23 10:06:47 +0800
categories: machine learning
comments: false
share: true
published: false
---
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

## 基本概念
#### 随机变量
- 连续型随机变量
- 离散型随机变量

#### 概率
出现某个值的可能性

## 连续型随机变量
对于连续型变量，它的值是无限的，于是对于某个点来讲，它的概率是零，即P(X=x)=0
#### 怎样定义概率？ 于是引入概率密度函数 
Probability Density Function (pdf):     
$$ P(a<X<b)=\int_{a}^{b}f(x)dx\quad 其中： 1. f(x) \geq  0 \quad 2.\int_{- \infty }^{ \infty }f(x)dx = 1 $$

## 重要的连续型随机变量分布
#### 正态(Normal)分布 又名高斯(Gaussian)分布
$$ X \sim \mathcal{N}(\mu,\,\sigma^{2})\, $$    
它的概率密度函数为：
$$ f(x) = P(X\geq x) = \frac{1}{\sqrt{2\pi \sigma ^{2}}} \mathrm{exp}\left (  - \frac{ \left ( x - \mu^{2}  \right )}{2\sigma ^{2}}  \right ) 其中： \mu \mathbb\in {R},\sigma ^{2} > 0 $$





## 离散型随机变量
