---
layout: splash
title: "Naive Bayes Algorithm - 朴素贝叶斯分类算法"
date:   2017-10-18 10:06:46 +0800
categories:
- machinelearning
tags:
- machinelearning
- bayesian
comments: true
share: true
publish: true
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

# 简介 
Naive Bayes 分类是基于贝叶斯定理和特征独立性假设的分类算法。

# 贝叶斯定理
- 条件概率    
抽扑克牌游戏，A（抽到方块）和B（抽到Queen）同时发生的概率    
$$ 1. P(A\bigcap B) = P(B) * P(A|B) $$    
$$ 2. P(A\bigcap B) = P(A) * P(B|A) $$     
**解释：**
1. 抽到方块Queen的概率 **等于** 抽到Queen的概率 **乘以** 当抽到一张牌是Queen的情况下，它是方块的概率。
2. 抽到方块Queen的概率 **等于** 抽到方块的概率 **乘以** 当抽到一张牌是方块的情况下，它是Queen的概率。

- 贝叶斯定理    
由上面的两个等式，我们可以得出     
$$ P(B) * P(A|B) = P(A) * P(B|A) $$   
即：   
$$ P(A|B) = \frac{P(B|A) * P(A)} {P(B)} $$     
**我们可以看出来，贝叶斯定理是描述P(A|B)和P(B|A)之间的关系的一条定理。**
**可以用贝叶斯定理由P(A|B)，结合P(A)和P(B)推导出P(B|A)。我们可以用已知的概率，去求得未知的概率**

# 应用举例
评论情绪分类（根据评论的内容判断是好评，还是差评）

    - P(A|B): 当评论里含有Good时，该评论为好评的概率。
    - P(A): 评论里含有Good的概率。
    - P(B): 评论为好评的概率。
    - P(B|A): 在好评的评论中含有Good的概率。


# 复杂一点的情况 （然而，真实情况并没有这么简单）
**往往条件不止一个，有多个**      
在 $$ X_{1},X_{2},X_{3} $$ 的情况下，Y发生的概率：   
$$ P(Y | X_{1},X_{2},X_{3}) = P(Y) * P(X_{1}|Y) * P(X_{2}|Y) * P(X_{3}|Y) $$    
**推导: **    
$$ P(Y \bigcap X_{1} \bigcap X_{2} \bigcap X_{3}) = P(X_{1} \bigcap X_{2} \bigcap X_{3}) * P(Y | X_{1},X_{2},X_{3}) $$  
    
# 经典案例 
![Bayesian 2]({{ site.baseurl }}/img/machinelearning/bayesian2.png){:width="500px"}    






