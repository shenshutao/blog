---
layout: splash
title: "应用工程统计学"
date:   2017-09-23 10:06:47 +0800
categories: machine learning
comments: false
share: true
published: true
---
<style type="text/css">
    table {
        width: 50%;
    }
</style>
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
# 应用工程统计学基础

## 基本概念
**随机变量** 是指变量的值无法预先确定，仅以一定的可能性(概率)取值的量。
- **连续型随机变量**： 对于随机变量X，若存在一个非负的可积函数f(x)，使得对任意实数x，有 $$\int_{-\infty }^{x}f\left ( u \right )du $$，则称X为连续性随机变量。
- **离散型随机变量**： 取值只有有限个或可列无穷个。

**概率** 是出现某个值的可能性。

## 连续型随机变量
对于连续型变量，它的值是无限的，于是对于某个点来讲，它的概率是零，即P(X=x)=0
#### 那么怎样定义概率？ 于是引入 
**概率密度函数: Probability Density Function (pdf)**     
$$ P(a<X<b)=\int_{a}^{b}f(x)dx\quad 其中： 1. f(x) \geq  0 \quad 2.\int_{- \infty }^{ \infty }f(x)dx = 1 $$

**累积分布函数: Cumulative Distribution Function (cdf)**      
$$ F\left ( x \right ) = P(X \leq x) = \int_{-\infty }^{x}f\left ( u \right )du $$


#### 平均值和方差 Mean and Variance
平均值 (期望值)： $$ \mu = E(X) = \int_{-\infty }^{\infty} xf(x)dx $$      
方差： $$ \sigma ^{2} = V(X) =  \int_{-\infty }^{\infty} (x - \mu)^2 f(x)dx = E(X^2 ) - \mu^2 $$    
标准方差为 $$ \sigma $$

### 重要的连续型随机变量分布：
#### 正态(Normal)分布 又名高斯(Gaussian)分布 Normal Distribution
**为什么重要：** 中心极限定理 The Central Limit Theorem\*      
$$ X \sim \mathcal{N}(\mu,\,\sigma^{2})\, $$    
它的概率密度函数为：
$$ f(x) = \frac{1}{\sqrt{2\pi \sigma ^{2}}} \mathrm{exp}\left (  - \frac{ \left ( x - \mu^{2}  \right )}{2\sigma ^{2}}  \right ) 其中： \mu \mathbb\in {R},\sigma ^{2} > 0 $$    
$$ \mu 是平均值， \sigma ^{2}是方差 $$

#### 标准正态分布 Standard Normal Distribution
当一个正态分布变量满足$$ 均值\mu = 0， 方差\sigma ^{2} = 1 $$， 我们把它称为标准正态分布变量，记做 **'Z'** 。    
$$ \Phi\left ( z \right ) = \mathbb{P}\left [ Z \leq z \right ] $$     

如果X是一个普通的正态分布变量，$$ 平均值为\mu， 方差为\sigma ^{2} $$，我们可以将其 **转化** 为标准正态分布变量：    
$$ Z = \frac{X - \mu }{\sigma } $$     
所以：    
$$ \mathbb{P}\left [ X\leq x \right ] = \mathbb{P}\left [ \frac{X - \mu }{\sigma } \leq \frac{x - \mu }{\sigma } \right ] = \Phi \left ( \frac{x - \mu }{\sigma } \right ) $$     
然后我们就可以使用标准正态分布表查询概率了。     


## 离散型随机变量
取值只有有限个或可列无穷个，比如投骰子的点数，调查的人数。    
#### 定义概率
**概率质量函数 Probability Mass Function**: 离散随机变量在各特定取值上的概率       
$$ f(x_{i}) = P(X = x_{i}) $$     

**累积分布函数: Cumulative Distribution Function**     
$$ F(x) = P(X \leq x) = \sum_{x_{i} \leq x}^{} f(x_{i}) $$      

#### 平均值和方差 Mean and Variance
平均值 (期望值)： $$ \mu = E(X) = \sum_{i=1}^{n} x_{i}f(x_{i}) $$      
方差： $$ \sigma ^{2} = V(X) =  E(X-\mu)^2 = \sum_{i=1}^{n} (x_{i} - \mu)^2f(x_{i}) = \sum_{i=1}^{n}x_{i}^2f(x_{i}) -\mu^2 $$    
标准方差为 $$ \sigma $$

### 重要的离散分布：
#### 二项分布 Binomial Distribution 又名贝努利（Bernoulli）分布
只有两种可能结果（0或1，成功或失败）的试验非常频繁，我们将它们称为贝努利试验。    
基于假设： 1. 每一次试验都是独立的，不会受到其他试验的影响。 2. 试验为某一值的概率是恒定的。    
比如著名的抛硬币实验，结果只有正面和反面，每一次投硬币都是独立的，为正面和反面的概率都恒定是0.5。    

**n次二项分布试验的结果中某一值出现的个数的几率**      
$$ f(x) = \binom{n}{x} p^{x} (1-p)^{n-x}, x = 0,1,...,n $$


## 中心极限定理 The Central Limit Theorem
在适当的条件下，大量相互独立的**随机变量**，其样本均值 $$ \bar{X} $$ （或者和）经适当标准化后依分布收敛于**正态分布**。      
有趣的是： **无论是什么分布的随机变量，都满足这个定理。**        

于是我们得到关于样本均值$$ \bar{X} $$的标准正态分布函数：       
$$ Z = \frac{\bar{X} - \mu }{\sigma / \sqrt{n}} \quad as \quad n \to \infty $$



## 单变量情况
#### 统计推断    
统计在研究现象的总体数量关系时，需要了解的总体对象的范围往往是很大的，有时甚至是无限的，而由于经费、时间和精力等各种原因，以致有时在客观上只能从中观察部分单位或有限单位进行计算和分析，我们要根据样本数据来推断总体数量特征。      
统计推断分为两个部分： **参数估计**和**假设检验**

#### 参数估计 
- 一般用样本均值估计总体均值     
样本均值函数: $$\mu = \frac{\sum_{i=1}^{N}x_{i}}{N} $$

- 一般用样本方差估计总体方差    
样本方差： $$ s^{2} = \frac{\sum_{i=1}^{n}(x_{i}-\bar{x})^{2}}{n-1} \quad (由于\bar{x}是由x_{i}计算出来的值，所以自由度为n-1)$$       
总体方差： $$ \sigma^{2} = \frac{\sum_{i=1}^{N}(x_{i}-\mu)^{2}}{N} $$    

**点估计**     

未知参数 $$ \theta $$ | 统计 $$ \hat{\Theta} $$ | 点估计 $$ \hat{\theta} $$
---- | --- | ---   
$$ \mu $$ | $$ \bar{X}= \frac{\sum X_{i}}{n} $$ | $$ \bar{x} $$ 
$$ \sigma^{2} $$ | $$ S^{2}=\frac{\sum (X_{i} - X)^{2}}{n-1} $$ | $$ s^{2} $$ 


#### 假设检验
基本思想是**小概率反证思想。**即小概率事件（P<0.01或P<0.05）在一次试验中基本上不会发生。     
具体步骤结合例子为下面7步：      
例子： 我们想知道一种固体推进器的线性燃烧速率是否为50cm/s，于是我们做了试验，得到一组数据，然后我们进行假设检验：            
1. 将问题提炼为统计问题: $$ \color{red}{我们关心的是总体均值 \mu} $$
2. 提出检验假设 Null hypothesis, $$ \color{red}{ H_{0}: \mu=50cm/s }$$
3. 提出备择假设 Alternative hypothesis, $$ \color{red}{ H_{1}: \mu\neq 50cm/s }$$
4. 确立检验统计量: $$ \color{red}{样本均值 \bar{X}}$$
5. 定义拒绝 $$ H_{0} $$的拒绝域: $$ \color{red}{如果假设成立，检验统计量\bar{X}落在拒绝域是一种小概率事件，不应该发生} $$
6. 根据样本，计算检验统计量的值: $$ \color{red}{计算 \bar{x}} $$
7. 判断是否拒绝: $$ \color{red}{如果\bar{x}在拒绝域内，拒绝检验假设H_{0}} $$



## 双变量情况

## 多变量情况
