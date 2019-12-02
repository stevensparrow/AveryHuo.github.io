---
title: Game Engine Architecture - Foundations Part3
categories:
- IT阅读
tags: 
- Game
---

## (3.1) C++ Review and Best Practive

imperative languages: C
object-oriented languages: C# , Java
scripting languages: python lua,perl
functional languages: Lisp, scheme, F# 

### Multiple Inheritance(MI)
Most C++ software developers avoid multiple inheritance completely or
only permit it in a limited form. 
> 多继承容易让结构混乱，提升技术难度，引发deadly diamond问题（当父类们存在相同函数时，子类不知道实现哪个？）
> 实际应用中，多继承应继承自无父的类对象
> Most C++ software developers avoid multiple inheritance completely or
only permit it in a limited form. A common rule of thumb is to allow only
simple, parentless classes to be multiply inherited into an otherwise strictly
single-inheritance hierarchy. Such classes are sometimes called mix-in classes
because they can be used to introduce new functionality at arbitrary points in
a class tree. 

![Deadly diamond](./img/1575255814499.png)
![Mix-in class](/img/1575255482902.png)

### Composition and Aggregation

组合和聚合
has-a, uses-a