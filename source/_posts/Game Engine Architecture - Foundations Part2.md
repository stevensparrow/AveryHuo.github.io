---
title: Game Engine Architecture - Foundations Part2
categories:
- IT阅读
tags: 
- Game
---

## (1.6) Runtime Engine Architecture

![Runtime Engine Architecture](./img/1574738644796.png)

>自底向上的顺序大概为：
>硬件层 
>驱动层
> 系统层 
>ＳＤＫ层
＞平台独立层
> 核心库
>资源库 
>　渲染，调试，物理检测，游戏平台基础
＞游戏级渲染，各上层动画机制，相机机制，ＡＩ机制
＞游戏逻辑层

### 操作系统层

分为PC与主机（游戏）系统，PC系统如windows 提供了一种线程的机制为分享硬件资源，而主机游戏一般来说则可占用所有的硬件资源，但这两者的差距在逐渐减少。

>Operating systems like Microsoft
Windows employ a time-sliced approach to sharing the hardware with multiple running programs, known as preemptive multitasking. 
>On a console, the game typically
“owns” the entire machine.
>So the gap between console and PC development is
gradually closing (for better or for worse).

###  3rd Party SDKS

> DirectX Opengl
> Havok, PhysX ODE etc.. 实现增强物理效果的SDK
> Boost++ C++标准库之一
> STL C++标准库之一
> Kynapse 游戏AI开发的中间件
> Granny, Havok Animation，处理动画骨骼等
> Euphoria， 小型的游戏开发套件：https://sourceforge.net/projects/euphoriasdk/

#### 数据结构与算法

C++ 库
1. STL : strings, data structures, stream-based I/O  
2. STLport :portable and optimized of STL
3. Boost :Powerful data structures and algorithms library
4. Loki :Powerful generic programming template library


#### 图形

>硬件图形库
> Glide  早期的3D图形SDK，针对Voodoo显卡。
> OpenGL widely used!
> DirectX Microsoft's 3D graphics SDK
> libgcm   更底层的接口针对PS3的图形硬件，OpenGL更高效处理的选择。
> Edge Naughty Dog 和Sony提供的PS3平台的库

#### 物理与碰撞

> Havok industrial-strength physics and collision engine.
> PhysX  NVIDIA
> Open Dynamics Engine.  open source

#### 角色动画

> Granny:
> In my opinion, the Granny SDK
has the best-designed and most logical animation API of any I’ve seen,
commercial or proprietary, especially its excellent handling of time

> Havok Animation
>  The line between physics and animation is becoming
increasingly blurred as characters become more and more realistic.

> Edge  PS3 from Sony

#### 生物力学角色模型 Biomechanical Character Models

>Endorphin and Euphoria. These are animation packages that produce
character motion using advanced biomechanical models of realistic human movement.
> Endorphin, is a Maya plug-in that permits animators to
run full biomechanical simulations on characters and export the resulting animations as if they had been hand animated
>Euphoria, is a real-time version of Endorphin intended
to produce physically and biomechanically accurate character motion at runtime under the influence of unpredictable forces.

> Endorphin， MAYA插件，执行动作的角色将运行一个完整的生物力学模拟同时导出动画。
> Euphoria,  在一些不可预测的因素影响下，将动作更精细的模拟表现出来。
https://space.bilibili.com/430600560/channel/detail?cid=75669


### Platform Independence Layer

>the platform independence layer ensures consistent
behavior across all hardware platforms.


### Rendering Engine
> The rendering engine is one of the largest and most complex components of
any game engine.

#### Low-Level Renderer
![Low-Level Renderer](./img/1574756479212.png)

> Graphics Device Interface
> DirectX, OpenGL

> The low-level renderer usually provides a viewport abstraction with an associated camera-to-world matrix and 3D projection parameters, such as field of view and the location of the near and far clip planes.

>  底层的渲染提供一个显示区域，关联到相机-世界和投影的参数。

#### Scene Graph / Culling Optimizations

> For very small game worlds, a simple frustum cull (i.e., removing objects
that the camera cannot “see”) is probably all that is required. For larger game
worlds, a more advanced spatial subdivision data structure might be used to
improve rendering efficiency by allowing the potentially visible set (PVS) of
objects to be determined very quickly. 

> potentially visible set (PVS)

> 理想状态下，底层渲染应该完全不关心spatial subdivision或scene graph的使用类型。 
>OGRE open source rendering engine (http://www.ogre3d.org) is a great example of this principle in action. OGRE provides a plug-and-play scene graph
architecture. Game developers can either select from a number of preimplemented scene graph designs, or they can provide a custom scene graph implementation.

#### Front End
> HUD, Heads-up Display
> 在顶层显示
> FMV, Full-Motion Video 动作完整的视频回放
This system is responsible for playing full-screen movies that have been recorded earlier.
> IGC, in-game cinematics system.  游戏内的视频，一般当玩家不可操作时显示




