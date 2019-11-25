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



