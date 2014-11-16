---
layout: post
title: windows7 + vmware 10 + ubuntu14.10下搭载Android开发环境
category: Android
tags: [Android]
excerpt: >
  此文不是手把手教你如何搭建，当然，如果在搭建过程中遇到什么问题，可以尝试在这里找找。
---

此文不是手把手教你如何搭建，当然，如果在搭建过程中遇到什么问题，可以尝试在这里找找。

linux获取root权限：

    sudo su --> password


安装vmware tools

    解压vmware-tools到/home/username文件夹
    
    切换到/home/username/vmware-tools...
    
    ./vmware-install.pl --prefix=/usr/vmware
    
    reboot

更新

    apt-get update
    
    apt-get upgrade

更新兼容32位库

    apt-get install -y libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1


安装jdk

    解压到/home/jusername目录
    
    mkdir /usr/java
    
    mv jdk1.7.0_67 /usr/java
    
    gedit /etc/profile
    
    export JAVA_HOME=/usr/java/jdk1.7.0_67
    export JRE_HOME=${JAVA_HOME}/jre  
    export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib  
    export PATH=${JAVA_HOME}/bin:$PATH
    
    修改默认JDK
    
    sudo update-alternatives --install /usr/bin/java java /usr/java/jdk1.7.0_67/bin/java 300  
    sudo update-alternatives --install /usr/bin/javac javac /usr/java/jdk1.7.0_67/bin/javac 300

安装adt

    使用谷歌集成adt，解压到/home/username目录
    
    mv adt-....... /usr
    
    配置安卓环境变量
    
    export ANDROID_HOME=/usr/adt/sdk
    export PATH=$ANDROID_HOME/platform-tools:$PATH
    export PATH=$ANDROID_HOME/tools:$PATH

下载SDK

    gedit /etc/hosts
    
    203.208.46.146 dl.google.com 
    203.208.46.146 dl-ssl.google.com
    
    
自动提示设置

    windows --> Preferences --> General --> Keys 
    搜索Word Completion取消Alt+/绑定。
    搜索Content Assist绑定Alt+/。

Ctrl+Alt+Up/Down

    System Settings --> keyboard --> Shortcuts --> Navigation --> Switch to workspace above/below


