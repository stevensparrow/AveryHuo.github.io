---
title: UI系统制作流程
categories:
- 公司
tags: 
---

#### 一、准备UI预制
先准备好效果图和资源图集
* 1.新建空场景，在目录下建好资源图集
* 2.找到 ***LoginUI.prefab*** ， 施入场景后，Unpack prefab completed完全解除关联
* 3.清空根结点的Animator组件和Reference Collector组件，并改名， 以 #Name#UI 的方式
* 4.清空Panel下所有内容，让结构保持为Bg, Panel两个一级子结点
*  *5.复制Bg结点，放入美术做好的效果图
* 5.根据UGUI规则完成预制制作
* 6.根结点添加Reference Collector Group组件
* 7.完成后交由特效师添加动画
* 8.将资源放入Addressable Groups的UI组里，右键使用Simplify Addressable Name, 将名字简化

#### 二、控制脚本
1.创建： 在Hotfix 建立文件夹，名字以功能命名，建立Compoents文件夹，新建控制脚本，命名以   UI#Name#Window的方式，如LoginUI，脚本名应为UILoginWindow.cs
2.类的规则以 UIClickWindow.cs为参考，
3.必须有的构造，以指明加载需要的预制名
```csharp
public UIClickWindow():base()
{
	mPrefabName = #Name#;//TODO
}
```
5.必须重写有如下函数：
```csharp
/// <summary>
/// 界面资源加载完成
/// </summary>
protected virtual void InitUI()
{
	//如有需要AddBehaviour
}

/// <summary>
/// 界面显示
/// </summary>
protected virtual void ResetUI()
{
}

/// <summary>
/// 界面关闭
/// </summary>
protected virtual void HideUI()
{
}

/// <summary>
/// 界面资源销毁
/// </summary>
protected virtual void UnInitUI()
{
	IsLoadDone = false;
}

/// <summary>
/// 界面Update更新
/// </summary>
public virtual void Update()
{

}
```

