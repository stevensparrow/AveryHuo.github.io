---
title: Python Core Programming Note 3
categories:
- Python笔记
tags: 
- Python
- Core Programming
- Note
---

## Multi-thread 

### Python 的 threading 模块
Python 提供了多个模块来支持多线程编程，包括 thread、 threading 和 Queue 模块等。程
序是可以使用 thread 和 threading 模块来创建与管理线程。 thread 模块提供了基本的线程和锁
定支持；而 threading 模块提供了更高级别、功能更全面的线程管理。使用 Queue 模块，用户
可以创建一个队列数据结构，用于在多线程之间进行共享。

>核心提示：避免使用 thread 模块
推荐使用更高级别的 threading 模块，而不使用 thread 模块有很多原因。 threading 模
块更加先进，有更好的线程支持，并且 thread 模块中的一些属性会和 threading 模块有冲突。
另一个原因是低级别的 thread 模块拥有的同步原语很少（实际上只有一个），而 threading
模块则有很多。
不过，出于对 Python 和线程学习的兴趣，我们将给出使用 thread 模块的一些代码。
给出这些代码只是出于学习目的，希望它能够让你更好地领悟为什么应该避免使用
thread 模块。我们还将展示如何使用更加合适的工具，如 threading 和 Queue 模块中的那
些方法。
避免使用 thread 模块的另一个原因是它对于进程何时退出没有控制。当主线程结束
时，所有其他线程也都强制结束，不会发出警告或者进行适当的清理。如前所述，至少
threading 模块能确保重要的子线程在进程退出前结束。
我们只建议那些想访问线程的更底层级别的专家使用 thread 模块。为了强调这一点，
在 Python3 中该模块被重命名为_thread。你创建的任何多线程应用都应该使用 threading 模
块或其他更高级别的模块。
