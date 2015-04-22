---
layout: post
keywords: NDK
title: "Android NDK系列（一）----NDK入门"
categories: [NDK]
tags: [NDK]
---
{% include codepiano/setup %}

本文通过创建一个最简单的[NDK Demo](https://github.com/kui2015/NDKTest)来介绍NDK的开发过程。

1. 创建一个Android Project "NDKTest",目录结构如下：

    <img src="/image/NDKTest_Package_Explorer.png" />

2. 在MainActivity.java中添加代码

	{% highlight java %}
		
		public native String helloJni();//需要在c代码里实现的方法

		static{
			System.loadLibrary("hello");//加载lib包
		}
		
	{% endhighlight %}

3. 创建jni文件夹

	打开终端，切换到当前项目目录

		mkdir jni //在当前目录下创建"jni"文件夹，此命令mac和windows通用

	其他命令

		ls//列出当前目录下的文件和文件夹 mac系统下
		dir//列出当前目录下的文件和文件夹 windows系统下

	Tip:

		在输入cd命令进入文件夹时，如果cd后面的字符串能唯一确定一个文件夹，则可通过tab键自动补全，mac、windows通用

4. 使用javah命令生成.h文件

	还是在当前项目目录下，输入

		javah -classpath bin/classes -d jni com.wujinkui.ndktest.MainActivity
		
	-classpath 用于装入类的路径，所以后面的bin/classes就是路径
	-d         输出目录，这里是jni
	-jni       默认的，不写也行

	运行成功后可以在jni文件夹下看到名为com_wujinkui_ndktest_MainActivity.h的头文件。

5. 编写c代码实现

	在jni文件夹下新建一个c文件，hello.c

	{% highlight c %}

	#include <jni.h>
	#include <string.h>
	#include <com_wujinkui_ndktest_MainActivity.h>

	JNIEXPORT jstring JNICALL Java_com_wujinkui_ndktest_MainActivity_helloJni
	  (JNIEnv *, jobject){
		return (*Env)->NewStringUTF(env, "Hello from JNI !");
	}

	{% endhighlight %}

6. Android.mk和Application.mk

	在官方的ndk samples里面有一个hello-jni的Project，将jni文件夹下的Android.mk和Applicaiton.mk拷贝到自己项目的jni文件夹下。

	Android.mk

	{% highlight ruby %}

	LOCAL_PATH := $(call my-dir)#给出当前文件的路径

	include $(CLEAR_VARS)

	LOCAL_MODULE    := hello#模块的名字，在MainActivity.java中load方法里的名字。系统会自动生成为libhello,load时不需要加"lib"
	LOCAL_SRC_FILES := hello.c#列出要编译的文件，文件之间可以用空格或Tab键进行分割,换行用"\"

	include $(BUILD_SHARED_LIBRARY)#编译时依赖的动态库

	{% endhighlight %}

	Application.mk

	{% highlight ruby %}

	APP_ABI := all#Application Binary Interface,因为代码很少，所以选择了all。一般用armeabi armeabi-v7a x86 和mips，其中前两个最常用

	{% endhighlight %}

7. ndk-build

	输入命令

		ndk-build

	编译成功后此时项目目录结构如下：

		<img src="/image/NDKTest_Package_Explorer_After_Compile.png" />

	如果编译失败，在重新编译前，要删除obj文件夹

8. 调用nativie方法

	在MainActivity.java的onCreate方法中添加

	{% highlight ruby %}

	Toast.makeText(this, helloJni(), Toast.LENGTH_LONG).show();

	{% endhighlight %}

	运行项目，弹出Toast--"Hello from JNI !"
