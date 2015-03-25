---
layout: post
title: Java -- 多线程
category: Java
tags: [Java]
excerpt: >
  Java多线程
---

##多线程

###Java实现多线程的两种方法
 
继承Thread类  
实现Runnable接口
    
####1. 继承Thread类

语法定义:
```Java
class ThreadClassName extends Thread{
    @override
    public void run(){
       //线程主体
    }
}
//开启线程
ThreadClassName threadClassName = new ThreadClassName();
threadClassName.run();
```
Demo:
```Java
class MyThread extends Thread{
    private String name;
    public MyThread(String name){
        this.name = name;
    }
    public void run(){
        for(int i = 0; i < 1000; i++){
            System.out.println(name + "运行, i = " + i);
        }
    }
}
public class ThreadDemo1{
    public static void main(String[] args) {
        MyThread myThread1 = new MyThread("zhangsan");
        MyThread myThread2 = new MyThread("lisi");
        MyThread myThread3 = new MyThread("wangwu");
        myThread1.start();
        myThread2.start();
        myThread3.start();
    }
}
```
注意：
```Java
public synchronized void start(){
	if(threadStatus != 0)
		throw new IllegalThreadStateException();
	...
	start0();
	...
}
private native void start0();
```
如果多次调用start()方法，会抛出IllegalThreadStateException异常。

####2.实现Runnable接口
语法定义:
```Java
class ThreadClassName implements Runnable{
    @override
    public void run(){
       //线程主体
    }
}
```
Demo:
```Java
class MyThread implements Runnable{
    private String name;
    public MyThread(String name){
        this.name = name;
    }
    public void run(){
        for(int i = 0; i < 1000; i++){
            System.out.println(name + "运行, i = " + i);
        }
    }
}
public class ThreadDemo1{
    public static void main(String[] args) {
        MyThread myThread1 = new MyThread("zhangsan");
        MyThread myThread2 = new MyThread("lisi");
        MyThread myThread3 = new MyThread("wangwu");
        Thread t1 = new Thread(myThread1);
        Thread t2 = new Thread(myThread2);
        Thread t3 = new Thread(myThread3);
        t1.start();
        t2.start();
        t3.start();
    }
}
```