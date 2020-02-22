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

1.1 LoadAssetAsyncHandle()
 * 以asset的形式加载资源不实例化，只返回相应资源句柄. [saveToCache]意为加载完的资源将直接记到缓存池，[isGlobal] 决定了是全局缓存池还是场景缓存池
**注意： [isGlobal]只在[saveToCache]为 true 时才会使用,用于保存在全局缓存池或对应场景的池子中**
```csharp
 ETTask<AsyncOperationHandle<T>> LoadAssetAsyncHandle<T>(string assetName, bool saveToCache = false, bool isGlobal = false)
```

>简单用法使用示例：(加载配置文件的Config预制)
>
>```csharp
> //获取加载完的句柄
> var configGOHandle = await ResourceLoaderComponent.Instance.LoadAssetAsyncHandle<GameObject>("Config");
>//从Handle中获取结果
> configGO = configGOHandle.Result;
> //当时即销毁此Handle
>ResourceLoaderComponent.Instance.ReleaseHandle(configGOHandle);


>深度使用示例：
>```csharp
>//预加载需要用的材质，设值记录到缓存, 且非全局资源
>await ResourceLoaderComponent.Instance.LoadAssetAsyncHandle<Material>("GrayMaterial",true,false);
> //从缓存加载对应的材质
> Material MAT_GARY = ResourceLoaderComponent.Instance.LoadFromCache<Material>("GrayMaterial", false);
>//从缓存删除对应的材质
> ResourceLoaderComponent.Instance.ReleaseFromCache("GrayMaterial",false,typeof(Material));
>```

1.2 LoadAssetsAsyncHandle()
* 以asset的形式加载资源不实例化，只返回相应此资源数组句柄. 区别于1.1接口，此接口可配置多一个label的参数指明资源标签。
**注意：如果保存到缓存中，则是一个数组，LoadFromCache时必须使用一个数组返回。**
```csharp
 ETTask<AsyncOperationHandle<IList<T>>> LoadAssetsAsyncHandle<T>(string assetName, ResourceLabel label = ResourceLabel.none, bool saveToCache = false, bool isGlobal = false)
```

>使用示例：
>```csharp
>var handle = await Game.Scene.GetComponent<ResourceLoaderComponent>().LoadAssetsAsyncHandle<GameObject>("HeadResSmallSize",ResourceLabel.ui);
>var userIcon = handle.Result[0];
>``` 
 

