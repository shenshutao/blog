---
layout: post
title: "Ensemble Learning - 集成学习 -onging"
date:   2017-10-01 10:06:46 +0800
categories: machine learning
published: false
---

# 集成学习
通过构建并结合多个学习器来完成学习任务。    
先产生一组‘个体学习器’(individual learner)，再用某种策略将他们结合起来。
<img src="{{ site.baseurl }}/img/machinelearning/ensemble01.png" alt="ensemble01" style="width: 300px;"/>   

- 学习器间存在强依赖关系，必须串行生成的序列化方法。 代表：Boosting
- 学习器间不存在强依赖关系，可同时生成的并行化方法。 代表：Bagging 和 Random Forest

# Boosting 
Boosting是一种常用的策略，可以将弱学习器提升为强学习器。其中弱学习器为准确率仅比随机好一点点的算法，而强学习器是准确率比较高的算法。 



# Bagging & Random Forest

# 结合策略

# 多样性