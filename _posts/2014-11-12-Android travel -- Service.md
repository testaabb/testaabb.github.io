---
layout: post
title: Android之旅（二） -- 四大组件之Service
category: Android
tags: [Android]
excerpt: >
  说过了Activity的生命周期，今天来说说Service。service是与Activity最相似的组件，它们都需要继承父类，都需要在
---

说过了Activity的生命周期，今天来说说Service。

Service是与Activity最相似的组件，它们都需要继承父类，都需要在AndroidManifest.xml中配置，区别就是service没有界面。在优先级上，Service比不活跃的Activity高。

####先来说说Service的生命周期，Service的生命周期相比于Activity来说简单一点，看图

![_config.yml]({{ site.baseurl }}/images/Service life cycle.png)  

左边是非绑定的: onCreate() --> onStartCommand() --> onDestory();
    onStartCommand()是用来替换onStart()方法的，谷歌建议大家用新方法onStartCommand(),但如果你去查看源码，会发现其实onStartCommand()方法是酱紫的: 关于onStartCommand()返回值的问题接下来再说。
``` java
public int onStartCommand(Intent intent, int flags, int startId) {
    onStart(intent, startId);
    return mStartCompatibility ? START_STICKY_COMPATIBILITY : START_STICKY;
}
```
现在来看右边的图：
右边是绑定的: onCreate() --> onBind() --> onUnbind() --> onDestory();

在Service的生命周期中，onCreate()方法只会被调用一次。而onStartCommand()方法可以被调用多次，onBind()等方法也只能调用一次，简单来说，除了onStartCommand()方法外，其他方法在一个生命周期中只能被调用一次。

####下面来说说如果两者混到一起的情况
此时只要记住有bind的时候不能stop;
如果调用了startService()，则只能在bind为零时用stopServivce()来结束Service;

####IntendService

Service运行在UI线程中，不能访问网络，也不能进行耗时的操作，否则会出现ANR。所以出现了IntenService。
IntentService是一个处理异步请求的类，它是Service的子类，我们可以同样使用startService(intent)来开启它，然后重写IntentService中的onHandleIntent()方法来执行一些耗时操作。
需要注意的是，IntentService类里面同样有onStartCommand()方法，你也可以重写onStartCommand()方法，这与普通Service类是一样的。在IntentService中，onStartCommand()方法先于onHandleIntent()方法执行。onHandleIntent()方法会在它执行结束后自动销毁。

####跨进程调用Service




####Service优先级


























