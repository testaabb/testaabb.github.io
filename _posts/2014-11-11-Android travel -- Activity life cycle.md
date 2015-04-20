---
layout: post
title: Android之旅（一） -- Activity生命周期
category: Android
tags: [Android]
---


  
终于可以开始写点东西啦。想起什么就写点什么，先来说说activity的生命周期吧。说到Activity的生命周期，就必须提到一张图。就是这个：

<img src="/images/Activity life cycle.png"/>
![_config.yml]({{ site.baseurl }}/images/Activity life cycle.png)
![_config.yml]({{ site.baseurl }}/images/Activity life cycle.gif) 

####来说说各个方法吧：

onCreate():创建Activity时被回调，只会被调用一次。  
onStart():启动Activity时被回调。  
onRestart()：重启Activity被回调。  
onResume():恢复Activity时被回调，此时Activity进入活动状态。注:onStart()方法之后一定会回调此方法。  
onPause():暂停（Activity页面失去焦点）Activity时被回调，暂停状态。  
onStop():停止Activity时被回调，停止状态。  
onDestory():销毁Activity时被回调，销毁状态。  
不理解没关系，继续往下看。  

####再来按照箭头说流程：
1. 中间主流程箭头：onCreate()-->onStart()-->onResume()-->onPause()-->onStop()-->onDestory()
    共6个流程，两两从中间对称，这个没什么好说的，打开Activity然后关闭（Back键），中间不进行任何多余操作，直接走完一个完整的生命周期。
2. 最右侧的箭头：从onStop()开始(在Activity界面按Home键后调用onStop())，再次进入Activity:onRestart()-->onStart()-->onResume()
3. 左侧onStop()开始的箭头：也是从onStop()开始,但是为什么调用了onCreate()呢？大家可以看左侧红色框内的文字“进程被杀死”，原来是整个进程被杀掉了(可以是用户行为，也可能是被系统回收)，这时再进入Activity则会从onCreate()开始。
4. 左侧onPause()开始的箭头：同理，在暂停状态进程被杀掉，再进入Activity则会从onCreate()开始。
5. 右侧onPause()开始的箭头：当Activity失去焦点后再次获得焦点，Activity进入活动状态调用onResume()方法。  

####现在说说在实际项目中的应用：
从流程中可以看出，onPause()是相对重要的，因为这是我们可以操作Activity的最后一道屏障。比如当前Activity处于活动状态，当电话进来，长按关机键弹出关机对话框或者在最近任务中结束掉此进程，onPause()方法都会被调用。所以我们可以再onPause()中保存数据，清除Text监听==。
