---
title: Game Engine Architecture - Foundations Part1 
categories:
- IT阅读
tags: 
- Game
---

## What is Game?

>In his excellent book, A Theory
of Fun for Game Design **a game to be an interactive experience that provides the player with an increasingly challenging sequence of patterns which he or she learns and eventually masters**.

>游戏： 一个交互性的经历提供一个玩家学习或将要学习的技能的挑战集合（持续提升的）

* soft real-time game & hard real-time game
  soft 意味着deadline不影响玩家，hard往往造成严重的后果。
  

## Game genres

### FPS

>first-person shooters aim to provide their players with the illusion of being
immersed in a detailed, hyperrealistic world

>First-person shooters typically focus on technologies such as:
>* efficient rendering of large 3D virtual worlds;
>* a responsive camera control/aiming mechanic;
>* high-fidelity animations of the player’s virtual arms and weapons;
>* a wide range of powerful handheld weaponry;
>* a forgiving player character motion and collision model, which often
gives these games a “floaty” feel;
>* high-fidelity animations and artificial intelligence for the non-player
characters (NPCs)—the player’s enemies and allies; and
>* small-scale online multiplayer capabilities (typically supporting up to
64 simultaneous players), and the ubiquitous “death match” gameplay
mode.

> 高效渲染3D虚拟世界
> 有响应式的相机控制与射击目标指向机制
> 高质量的玩家手臂和武器控制
> 丰富的装备选择
> 丰富的人物动画库和碰撞模型
> 非玩家（NPC）的高质量动作和人工智能
> 小型的多人同屏（<64）和频繁的角色死亡重生的游戏机制

### Platformers and Other Third-Person Games

> Technologies specifically:
> * moving platforms, ladders, ropes, trellises and other interesting locomotion modes;
> * puzzle-like environmental elements;
> * a third-person “follow camera” which stays focused on the player character and whose rotation is typically controlled by the human player via
the right joypad stick (on a console) or the mouse (on a PC—note that
while there are a number of popular third-person shooters on a PC, the
platformer genre exists almost exclusively on consoles); and
> * a complex camera collision system for ensuring that the view point never
“clips” through background geometry or dynamic foreground objects

> 移动平台，楼梯等模块
> 场景的混淆视听的组件
> 第三人称使用的相机跟随
> 复杂的相机机制以显示当前游戏所需的空间

### Fighting Games

> Efforts on:
> * a rich set of fighting animations;
>*  accurate hit detection;
>* a user input system capable of detecting complex button and joystick
>combinations; and
>*  crowds, but otherwise relatively static backgrounds

> State-of-the-art fighting games:
>*  high-definition character graphics, including realistic skin shaders with
subsurface scattering and sweat effects;
>* high-fidelity character animations; and
>*  physics-based cloth and hair simulations for the characters.

> 丰富的对战性的动画集
> 精准的碰撞检测
> 连招所用的组合键设计
> 观众相关的人群背景设计

> 高质量的人物画面及皮肤shader支持
> 高质量的动画
> 头发衣服的模拟


### Racing Games
>Some of the technological properties of a typical racing game include the
following techniques:
>* Various “tricks” are used when rendering distant background elements,
such as employing two-dimensional cards for trees, hills and mountains.
>* The track is often broken down into relatively simple two-dimensional
regions called “sectors.” These data structures are used to optimize
rendering and visibility determination, to aid in artificial intelligence
and path finding for non-human-controlled vehicles, and to solve many
other technical problems.
>*The camera typically follows behind the vehicle for a third-person perspective, or is sometimes situated inside the cockpit first-person style.
>*When the track involves tunnels and other “tight” spaces, a good deal
of effort is often put into ensuring that the camera does not collide with
background geometry

>  背景元素的各种2D的以假乱真的方法
>  赛道的设计，使用2维的Sectors的数据结构，用于优化渲染和视觉效果，也可辅助设计AI的寻路等
>  相机的视角以塞车后方的第三方人称或驾驶室的第一人称角色

### Real-Time Strategy(RTS)

> Include the following techniques:
>* Each unit is relatively low-res, so that the game can support large numbers of them on-screen at once.
>* Height-field terrain is usually the canvas upon which the game is designed and played.
>* The player is often allowed to build new structures on the terrain in
addition to deploying his or her forces.
>* User interaction is typically via single-click and area-based selection of
units, plus menus or toolbars containing commands, equipment, unit
types, building types, etc.

> 每一个单元都占有相对少的资源，以便支持更多单元的同屏
> 高地的地型常用于场景中
> 玩家可自己支配自己的势力在地图，如创建一些建筑等
> 交互模式传统上来说是用单击或区域选择


### Massively Multiplayer Online Games (MMO)

