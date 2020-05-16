---
title: DOTS-事件
categories:
- Unity
---

### 方式一、使用NativeQueue循环检测
* 1. 获取JOB可写的多线程NativeQueue对象
```c#
NativeQueue<PipePassedEvent>.ParallelWriter eventQueueParallel = eventQueue.AsParallelWriter();
```

* 2. 发出事件
```c#
eventQueueParallel.Enqueue(new PipePassedEvent());
```

* 3. 事件机
```c#
while (eventQueue.TryDequeue(out PipePassedEvent evnt))
        {
            //Debug.Log("Get EVENT!!");
            OnPipePassed?.Invoke(this, EventArgs.Empty);
        }
```

4.接收事件
```c#
World.DefaultGameObjectInjectionWorld.GetOrCreateSystem<PipeMoveSystem_Done>().OnPipePassed += TestingDOTSEvents_OnPipePassed;
```
