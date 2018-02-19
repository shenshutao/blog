---
layout: splash
title: "Java 操作 复杂度汇总"
date:   2017-11-17 19:06:46 +0800
categories: java
comments: false
share: true
publish: false
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
# Java 操作 复杂度汇总     
## 排序算法

| 排序算法 | 英文名 | 时间复杂度 平均 | 时间复杂度 最差 | 时间复杂度 最好 | 空间复杂度 | 稳定性 | 复杂性 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 归并排序 | Merge sort | $$ O(nlog_{2}n) $$ | $$ O(nlog_{2}n) $$ | $$ O(nlog_{2}n) $$ | O(n) | 稳定 | 较复杂 |
    
[Link](http://www.cnblogs.com/nannanITeye/archive/2013/04/11/3013737.html)


## Collection增删查找
### List 性能

| 类 | get() | add() | remove() |
| --- | --- | --- | --- |
| ArrayList | O(1) | O(1) | O(n) |
| LinkedList | O(n)| O(1)| O(n) |

### Set 性能

| 类 | get() | add() | remove() | contains() | next() |
| --- | --- | --- | --- | --- | --- |
| HashSet | O(1) | O(1) | O(1) | O(1) | O(h/n) |
| TreeSet | O(log n)| O(log n)| O(log n) | O(log n) | O(log n) |


