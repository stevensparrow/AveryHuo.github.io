---
title: DrawCall优化
categories:
- 公司
tags: 
---

#### 系统UI的DrawCall优化方案：

> 造成dc增加有：
> 1. 不同级别的放置Image, 即两个同图集的image放在不同的两个button的子组件。
> 2. Mask会占两个dc
> 3. 不同Layout组件下的image也会造成不同合批，产生dc.

解决方案：
1. 同图集image尽量同组同级放置
2. 使用reckmask2d替代mask组件
3. 不要过多在同图集图片间使用layout组件


### 模型批处理

动态批处理：
一定要相同材质，不能有负数的scale，这样将自动进行动态批处理

静态批处理

gpu instancing:

