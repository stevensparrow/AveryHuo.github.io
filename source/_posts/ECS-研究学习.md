---
title: DOTS-研究学习
categories:
- Unity
---

### What is DOTS?

DATA-ORIENTED TECH STACK
多线程式数据导向型技术堆栈

1. 核心-高性能
充分利用多核处理器，多线程，让游戏运行速度更快。
组成部分如下：
* C# 任务系统， Job System，用于高效运行多线程代码
* 实体组件系统，ECS， 默认编写的高性能代码的框架结构
* Burst编译器，用于生成高度优化的本地代码

Job System 与ECS是独立的，两者结合实际才能发挥最大优势。

2. Job System

* 在Job System之前，unity 仅在内部支持多线程，外部都必须运行在主线程上
* C#虽然支持多线程，但在unity中只处理数据，如网络消息，下载等等，且在线程中调用Unity的API是不行的。
* 有了Job System,可以充分利用多核CPU，比如在多线程中修改Transform等
* 例：MMO游戏判断碰撞，大量同步角色坐标，大量血条飘字等较为适合
* 不必过于担心线程安全，加锁的问题
* 配合Burst更佳

2.1 HPC# -High Performance C#

介绍：
* IL2Cpp虽然将IL转成C++，但实际还是模拟了.NET的垃圾回收，效率并非等同C++
* 使用NativeArray<T>代替T[]，数据类型包括了值类型和其他类型指针
* NativeArray可以在C#层分配 C++中的对象，主动释放而不进行C#的垃圾回收。

Burst性能对比：
* .Net Code 比C++慢2倍
* Mono比.NET Code慢3倍
* IL2CPP与.NET Code相当
* Burst将比C++运行更快。

http://aras-p.info/blog/2018/03/28/Daily-Pathtracer-Part-3-CSharp-Unity-Burst/

2.2 代码使用

* 数据类型只能是值类型和其他类型的指针
* 不能使用引用类型，如T[]数组就不能在job中使用，应用HPC#的NativeArray代替



