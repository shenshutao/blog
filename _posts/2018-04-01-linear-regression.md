---
layout: splash
title: "线性回归 Linear Regression"
date:   2018-04-1 10:06:47 +0800
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
# 线性回归
上接 应用工程统计学基础
* 目录    
{:toc}

# 一元线性回归
一元线性回归预测是指成对的两个变量数据的散点图呈现出直线趋势时，采用最小二乘法，找到两者之间的经验公式，即一元线性回归预测模型。    

## 背景和模型
前提假设：两个变量数据的散点图呈现出直线趋势。（之后我们通过假设验证来证明）   
回归分析：对两个不确定关系的变量进行统计学分析建模。（回归一般理解为向均值回归）   
经验公式：根据观察推断出公式，而不是根据理论。   

一元线性回归模型 $$Y=\beta_{0}+\beta_{1}x+\varepsilon$$ 包括两个部分
- 确定性部分，$$y=\beta_{0}+\beta_{1}x$$
- 不确定性部分，误差 $$\varepsilon$$。 

对误差的假设（之后讨论如何对误差进行分析，见**模型充分性检查**）
- 所有误差$$\varepsilon_{1}...\varepsilon_{n}$$都是随机和独立的
- 所有误差$$\varepsilon_{1}...\varepsilon_{n}$$均值为0
- 所有误差$$\varepsilon_{1}...\varepsilon_{n}$$有相同方差$$\sigma^{2}$$
- 所有误差$$\varepsilon_{1}...\varepsilon_{n}$$呈正态分布

基于对误差的假设，我们可以知道
- $$Y_{i}$$期望值：$$E(Y_{i})=E(\beta_{0}+\beta_{1}x_{i}+\varepsilon_{i})=\beta_{0}+\beta_{1}x_{i}+E(\varepsilon_{i})=\beta_{0}+\beta_{1}x_{i}$$
- $$Y_{i}$$方差：$$V(Y_{i})=V(\beta_{0}+\beta_{1}x_{i}+\varepsilon_{i})=V(\varepsilon_{i})=\sigma^{2}$$     

我们发现$$Y_{i}$$服从正态分布：$$N(\beta_{0}+\beta_{1}x_{i},\sigma^{2})$$

## 模型参数估计
一般来说，$$\beta_{0}和\beta_{1}$$都是未知的，我们可以根据样本来估计他们的值。     
既然是估计值，大家都戴上帽子，等式变为$$\hat{Y}=\hat{\beta}_{0}+\hat{\beta}_{1}x$$    

### 一般使用最小二乘法，估计$$\beta_{0}，\beta_{1}$$
找出$$\hat{\beta}_{0}和\hat{\beta}_{1}$$使总的误差平方和最小。即$$Minimize\;f(\hat{\beta}_{0},\hat{\beta}_{1})=\sum_{i=1}^{n}\varepsilon_{i}^{2}=\sum_{i=1}^{n}(y_{i}-\hat{\beta}_{0}+\hat{\beta}_{1}x_{i})^{2}$$  
求极值，进行求导，运算，得到结果：    
$$\hat{\beta}_{0}=\bar{y}-\hat{\beta}_{1}\bar{x}$$    
$$\hat{\beta}_{1}=\frac{S_{xy}}{S_{xx}}$$    
于是我们可以先求得$$\hat{\beta}_{1}$$，再求得$$\hat{\beta}_{0}$$。    

### 然后估计$$\sigma^{2}$$
我们定义$$SSE=\sum_{i=1}^{n}e_{i}^{2}=\sum_{i=1}^{n}(y_{i}-\hat{y}_{i})^{2}$$。   
那么$$\hat{\sigma}^{2}=MSE=\frac{SSE}{N-2}$$ （因为失去两个自由度$$\hat{\beta}_{0}，\hat{\beta}_{1}$$）

### 问题产生了：这些估计值不好? 
我们知道$$\hat{\beta}_{0}，\hat{\beta}_{1}$$是根据样本计算出来的估计值，那么根据同一总体的不同的样本我们会得到不一样的$$\hat{\beta}_{0}，\hat{\beta}_{1}$$。

### 分析 $$\hat{\beta}_{1}$$
因为$$\varepsilon_{i}$$服从正态分布，所以$$y_{i}$$服从正态分布，由于$$\hat{\beta}_{1}=\frac{S_{xy}}{S_{xx}}，\hat{\beta}_{1}和y_{i}们为线性关系$$，我们得出：
- $$\hat{\beta}_{1}$$服从正态分布
- 期望值 $$E(\hat{\beta}_{1})=\beta_{1}$$
- 方差 $$Var(\hat{\beta}_{1})=\sigma_{\hat{\beta}_{1}}^{2}=\frac{\sigma^{2}}{\sum (x_{i}-\bar{x})^{2}}=\frac{\sigma^{2}}{S_{xx}} $$.  

    从方差等式$$Var(\hat{\beta}_{1})=\frac{\sigma^{2}}{\sum (x_{i}-\bar{x})^{2}}$$中，我们可以知道，为了减小$$\hat{\beta}_{1}$$的方差，从分母上看，拿更大的样本，分母会变得更大，能有效减小$$Var(\hat{\beta}_{1})$$。当然在相同条件下，样本x点在合理范围内分布更广的话，势必$$\sum (x_{i}-\bar{x})^{2}$$也会更大。    

### 用$$\hat{\beta}_{1}$$来判断x和y是否线性相关
既然知道了$$\hat{\beta}_{1}～N(\beta_{1},\sigma^{2}/S_{xx})$$，我们可以进行假设检验。   
用T-test来假设验证他的均值$$H_{0}: \beta_{1} = 0$$, 如果无法拒绝$$\beta_{1}$$等于零，则意味着无法肯定x和y的线性关系。   
$$H_{0}: \beta_{1} = 0$$    
$$H_{1}: \beta_{1} \neq 0$$  
测试的统计量:   
$$T_{0}=\frac{\hat{\beta}_{1}-0}{\hat{\sigma}/\sqrt{S_{xx}}}$$     
检验方式：1.P值 2.给定显著性水平 3.置信区间     
（我们在用工具建立线性回归模型时候，工具都会帮我们自动进行这个T检验，以判断x和y的线性关系是否significant。）

### 分析$$\hat{\beta}_{0}$$, 虽然其实大家并不怎么关心$$\beta_{0}$$
因为$$\hat{\beta}_{1}$$服从正态分布，然后$$\hat{\beta}_{0}$$和他是线性关系，所以$$\hat{\beta}_{0}$$也是服从正态分布。    
$$\hat{\beta}_{0}～N(\beta_{0},\sigma_{\hat{\beta}_{0}}^{2})$$

## 模型整体评估
### 评估策略 R-Square
线性回归模型的整体评估用了一个很有趣的思路，$$R^{2}$$，我们看模型解释了多少的方差，具体如下     
- 模型方差 $$SSE=\sum_{i=1}^{n}(e_{i}^{2})=\sum_{i=1}^{n}(y_{i}-\hat{y}_{i})^{2}$$
- 样本整体方差 $$SST=\sum_{i=1}^{n}(y_{i}-\bar{y})^{2}$$

然后$$R^{2}=1-\frac{SSE}{SST}$$，这个值高意味着我们的模型消除了y的不确定性，这个值低则意味着我们的模型不好。   
在模型输出中，一般我们还可以看到修正以后的$$R_{adj}^{2}=1-\frac{MSE}{MST}=1-\frac{SSE/(n-2)}{MST/(n-1)}$$，会比$$R^{2}$$小一点点，毕竟n-2 < n-1 （当然这是一元线性模型，多元模型就不仅仅是n-2了，那是n-p-1）    

### 方差分析 ANOVA 
对等式稍微做一下变形$$R^{2}=1-\frac{SSE}{SST}=\frac{SST-SSE}{SST}=\frac{SSR}{SST}$$，SSR是regression模型解释的方差。    
即$$SS_{T}=\sum_{i=1}^{n}(y_{i}-\bar{y})^{2}=\sum_{i=1}^{n}(\hat{y}_{i}-\bar{y})^{2}+\sum_{i=1}^{n}(y_{i}-\hat{y}_{i})^{2}=SS_{R}+SS_{E}$$    
$$\color{red}{如果\beta_{1}=0， 则}$$
用ANOVA来假设检验两个方差是否相等，如果模型能解释的方差大于不能被模型解释的方差，那我们认为这个模型是有效的。


## 模型充分性检查
## 置信区间

# 多元线性回归
