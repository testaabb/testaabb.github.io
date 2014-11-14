---
layout: post
title: Android之旅（三） -- AsyncTask
category: Android
tags: [Android]
excerpt: >
  今天来说一说AsyncTask
---

今天来说一说AsyncTask

####AsyncTask的实现

1.创建AsyncTask的子类，为三个泛型参数指定类型，如不需要则为void。
    三个参数
        Params：输入类型
        Progress：进度值类型
        Result：返回值类型
        
2.必须实现doInBackground()方法，可根据需要实现onProgressUpdate(),onPreExecute(),onPostExecute()方法。这些方法只能由系统负责调用。  

3.在主线程中调用AsyncTask实例的execute()方法。

####其他有的没的

如果要在AsyncTask的子类里操作UI，可将Activity的Context在实例化子类时当做参数传递过去。  
多次执行会报java.lang.IllegalStateException: Cannot execute task: the task is already running.bug，当然，如果每次都是新new出来的就没问题，不过新任务会在旧任务执行完毕后再开始。


```java
	if(asyncTaskTest.getStatus() == AsyncTask.Status.RUNNING)
		asyncTaskTest.cancel(true);
```
