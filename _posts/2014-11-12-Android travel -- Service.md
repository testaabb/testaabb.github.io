---
layout: post
title: Android之旅（二） -- 四大组件之service
category: Android
tags: [Android]
excerpt: >
  说过了Activity的生命周期，今天来说说service。

service是与Activity最相似的组件，它们都需要继承父类，都需要在AndroidManifest.xml中配置，区别就是service没
---

说过了Activity的生命周期，今天来说说service。

service是与Activity最相似的组件，它们都需要继承父类，都需要在AndroidManifest.xml中配置，区别就是service没有界面。

####先来说说service的生命周期，service的生命周期相比于Activity来说简单一点，看图

![Alt text](./1415768381287.png)

左边是非绑定的: onCreate() --> onStartCommand() --> onDestory();
    onStartCommand()是用来替换onStart()方法的，谷歌建议大家用新方法onStartCommand(),但如果你去查看源码，会发现其实onStartCommand()方法也是调用onStart()的。
右边是绑定的: onCreate() --> onBind() --> onUnbind() --> onDestory();
同Activity，onCreate()方法只会被调用一次。而onStartCommand()方法可以被调用多次，onBind()等方法也只能调用一次，简单来说，除了onStartCommand()方法外，其他方法在一个生命周期中只能被调用一次。

####下面来说说比较复杂的，两种混合着用。