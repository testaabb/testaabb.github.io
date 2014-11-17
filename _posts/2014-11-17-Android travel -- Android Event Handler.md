---
layout: post
title: Android之旅（五） -- 事件处理机制
category: Android
tags: [Android]
excerpt: >
  安卓事件处理机制                      
---

安卓事件处理机制：
	基于监听的事件处理
	基于回调的事件处理

监听的处理模型：
	Event Source（事件源）：事件发生的场所，通常就是各个组件。如button，menu等
	Event（事件）：由系统封装。
	Event Listener（事件监听器）：监听事件源所发生的事件，并作出相应的相应。
	
View类的内部接口：  
	OnClickListener  
	OnCreateContextMenuListener  
	OnFocusChangeListener  
	OnKeyListener  
	OnLongClickListener  
	OnTouchListener  
	
实现事件监听器：  
	内部类形式  
	外部类形式  
	Activity本身作事件监听器  
	
```java
btn.setOnClickListener(this);  
	@Override  
	public void onClick(View v){  
	...;  
}  
```
	匿名内部类形式  
	直接绑定到标签（增加耦合，不建议）  
  
基于回调的事件传播：  
	组件的事件监听器 --> 事件回调方法 --> 组件所在的Activity（该Activity包含的所有组件）  
	
获取系统的Configuration：Configuration config = getResources().getConfiguration();  
设置屏幕方向：setRequestOrientation(int);  
重写onConfigurationChanged(Configuration newConfig);  
