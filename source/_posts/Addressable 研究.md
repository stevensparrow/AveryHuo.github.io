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

Data Builders：在Addressable窗口菜单中能够选择的在编辑器下的数据构建模式，一般来说附带的这几个已经可以满足大部分要求，你也可以新建适合自己项目的模式。
Fast Mode：加载资源不通过资源包，直接使用AssetDatabase加载。
Virtual Mode：会形成AssetBundle布局，但是不需要打包，加载资源通过ResourcesManager加载，并且可以在RM Profiler中查看包体布局。
Packed Mode：需要额外步骤打包AssetBundle，运行时资源也是在AssetBundle中进行加载。

## 迁移指南

![从自己框架移植](/img/1579081015473.png)

![从Resources移植](/img/1579081031342.png)


## 使用注意项：
1.每调用一次Addressables.Instantiate方法，会将该Asset的引用计数加一；而Addressables.ReleaseInstance会减少这个引用计数。如果你使用Object.Destroy释放了它，则原始资源会一直存在于内存中。所以应当避免使用Object.Destroy方法了~
2.非使用 Addresables.Instantiate 方法实例化出来的对象，如使用Unity自带的Instantiate实例出来的对象，也可以使用Addressables.ReleaseInstance来释放，这并不会对计数有影响，只是单纯的释放。
3.任何通过Addresables.Instantiate 方法实例化出来的对象，在切换场景的时候，如果没有标记为 DontDestroyOnLoad ,则会被自动调用Addressables.ReleaseInstance来释放掉。


## 总结：

> 指定本地和服务端资源：设置为Build RemoteCatalog时，才为服务端资源，即不跟随包打出。
> build出的包带资源，但此资源要热更怎么办？
 1. 先将资源标注成Local build的路径形式（一定要成对），这样打出的包就会被带到手机包里
 2. Content Update Restriction一定要选上Cannot Change Post Release， 指明此资源是固定资源在外里的
 3. 出过一个版本后，使用Tools下的Check for Content Update Restriction，找出变更的固定资源到Content Update的分组中
 4. 使用Build -> Update Previous build 更新之前的版本即可完成来更新。
> 那么如果已经指明此为remote资源的话，如果更新呢？ 那很简单了，直接使用Build -> Update previous build就行了。因为路径已经指明到远端，此时打开会自动更新成最新的。