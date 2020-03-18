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
* 使用NativeArray代替T[]，数据类型包括了值类型和其他类型指针
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

![enter description here](/img/1584498872491.png)

> IJob与IJobParallelFor
> IJob是一个一个的开线程任务，顺序执行的，所以正确性有保证
> 如果想让线程真正并行，则应使用JobParallelFor。这样并行后的数据就不会有前后依赖关系。
> 使用ReadOnly标记的数据，只读后让Job不为其加锁。
> 默认的数据是Read/Write的，这样在改变数据后，Job一定会等它。
> 加解锁unity已经做好了，不需要自己实现逻辑。
> 
![enter description here](/img/1584499275880.png)

3.Burst编译器

原理
* 以开源LLVM为基础的后端编译技术
* 原理的5个步骤：源代码》前端》优化器》后端 》机器码
* LLVM定义抽象语言IR，前端负责将源代码（C#）翻译成IR，优化器优化，后端将IR生成目标语言（机器码）。
* IR的存在，所以LLVM支持众多语言
* LLVM对C#的GC支持不好，目前burst只支持值类型。

内存别名
* 之前的编译器无法知道运行时两个指针指向同一个地址的情况，编译出的代码必然要占用额外寄存器多次拷贝，无法优化。
* NativeArray的API禁止限制了内存别名，