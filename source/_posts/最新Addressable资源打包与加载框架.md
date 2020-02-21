---
title: 最新Addressable资源打包与加载框架
categories:
- 公司
tags: 
- Addressable
---

#### 一、Addressable介绍

Addressable是Unity最新推出且正式发布的资源管理系统，内含引用计数管理，快速资源热更，资源性能查看器，资源冗余工具等等，据官方的说法，这就像当初AssetBundle取代Resources一样，Addressable就是为了取代直接使用AssetBundle而生。

#### 二、Addressable内置接口介绍

 ##### 1. 加载接口

```csharp
Addressables.LoadAssetsAsync()
```

