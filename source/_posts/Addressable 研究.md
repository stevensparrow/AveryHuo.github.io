---
title: Addressable 研究
categories:
- Unity学习
tags: 
- Unity学习
---

## 什么是Addressable？
![什么](/img/1579072055300.png)

## Addressable的实例函数

![实例函数](/img/1579077588215.png)

## 以label形式加载

![以label加载](/img/1579078623846.png)

## 模式选择

![模式](/img/1579078890824.png)

> Fast Mode:editor 模式
> Virtual Mode: 本地，虚拟服务端环境
> Packed: 纯打包的环境

## 迁移指南

![从自己框架移植](/img/1579081015473.png)

![从Resources移植](/img/1579081031342.png)


## 使用注意项：
1.每调用一次Addressables.Instantiate方法，会将该Asset的引用计数加一；而Addressables.ReleaseInstance会减少这个引用计数。如果你使用Object.Destroy释放了它，则原始资源会一直存在于内存中。所以应当避免使用Object.Destroy方法了~
2.非使用 Addresables.Instantiate 方法实例化出来的对象，如使用Unity自带的Instantiate实例出来的对象，也可以使用Addressables.ReleaseInstance来释放，这并不会对计数有影响，只是单纯的释放。
3.任何通过Addresables.Instantiate 方法实例化出来的对象，在切换场景的时候，如果没有标记为 DontDestroyOnLoad ,则会被自动调用Addressables.ReleaseInstance来释放掉。