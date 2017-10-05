---
layout: post
title: "Object Oriented Design Patterns 设计模式 - ongoing"
date:   2017-09-28 12:06:46 +0800
categories: Design Pattern
---

# Briefing 简介
设计模式是一套被反复使用的、多数人知晓的、经过分类编目的、代码设计经验的总结。 它代表了最佳实践。  

# OO Design Principles 面向对象设计原则 - SOLID
1. Single Responsibility Principle 单一职责原则
对象应该仅具有一种单一功能。低耦合，高内聚，职责过多会导致引起对象变化的原因复杂，互相依赖，互相影响。     
“就像一个人身兼数职，而这些事情相互关联不大，甚至有冲突，那他就无法很好的解决这些职责，应该分到不同的人身上去做才对。” 

2. Open Close Principle 开放封闭原则
软件体应该是对于扩展开放的，但是对于修改封闭的。
类可以被继承扩展满足不同的需求，但是类的内部结构是稳定的，不会被需求影响。
这个规则已存在于Java语法中，所有的Java程序都是在扩展Java那些SDK类上建立的，然后SDK不允许被修改。

3. Liskov's Substitution Principle 里式替换原则
子类能够替换其基类。 这是关于继承机制的设计。
这个规则已经存在于Java语法中

4. Interface Segregation Principle 接口分离原则
多个特定客户端接口要好于一个宽泛用途的接口

5. Dependency Inversion Principle 依赖倒置原则
依赖于抽象而不是一个实例，即父类不能依赖子类，它们之间还要有抽象类。 因为抽象比较稳定，实体容易变化。 且易于分工合作，高层模块使用抽象，底层模块实现抽象。    
经典例子： Dao -> DaoHibernate  /  Dao -> DaoMyBatis      
Java中有Interface (接口) 或者 Abstract （抽象类）

----

# Creational Patterns 创建型模式
1. Factory Pattern 工厂模式
当创建一些复杂对象的时候，特别是创建步骤比较复杂的类型。   
优点： 
- 简化复杂对象创建过程。
- 屏蔽产品的具体实现，调用者只关心产品的接口。
缺点：
-  

2. Abstract Factory 抽象工厂模式
3. Singleton 单例模式
 Ensure that only one instance of a class is created and Provide a global access point to the object.
 保证一个类仅有一个实例，并提供一个访问它的全局访问点。
 **场景实例:** 1. 一个人的 

4. Builder 建造者模式
5. Prototype 原型模式
6. Object Pool 

----

# Behavioral Patterns 
1. Chain of Responsibility
2. Command
3. Interpreter
4. Iterator
5. Mediator
6. Memento
7. Observer
8. Strategy
9. Template Method
10. Visitor
11. Null Object

----

# Structural Patterns
1. Adapter
2. Bridge
3. Composite
4. Decorator
5. Flyweight
6. Proxy
