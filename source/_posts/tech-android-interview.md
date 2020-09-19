---
title: Android面试
date: 2020-08-14 15:57:53
tags:
---

> 其实说是android面试，其实更多的会问到许多java的知识，毕竟基础嘛，实习生面试还是以基础为主（我猜的），然后这篇文章会融合之前写过的东西，从面试流程开始。此文的面试题有的是我经历过的，有的是网上的一些，为方便复习总结，收集于此。学术不精，如有错误，请与我联系改正 ( •̀ ω •́ )✧

## 前言


> 简单写写面试流程 , 我遇到过的好几个都是这样的 QAQ

### 自我介绍

面试官您好，我叫XXX，来自XXX（学校）XX学院，XX公司我一直非常尊敬的公司，这一次我应聘的是XXX（职位），平常喜欢XXX（和职位有关的兴趣，比如写博客什么的），希望能过加入XX公司从事相关工作

### 介绍项目

> 如果你有写的话

通常分为几步
1. 在项目里担任了什么职位，完成了什么
2. 涉及到的技术，这其中会深入的问你和项目相关的问题，比如，我的项目里用到了`okhttp`，面试官会问你有没有阅读过`okhttp`的**源码**啊，大概怎么实现的啊，之类的问题
3. 有什么感悟，遇到过什么难题 , 有些地方的实现为什么要这样实现而不是那样实现啊

## Android

### Android的四大组件
> 所有android应用都是由四大组件组成的：Activity，BroadcastReceiver，Service，ContentProvider

- Activity：最基本的组件，一个就是一个屏幕，通常都被实现为一个独立的类
- BroadcastReceiver：使用它对外部事件进行过滤，接收并做出响应
- Service：一个服务是具有一个较长生命周期且没有用户界面的程序。
- ContentProvider：使一个应用程序的指定数据集可以提供给其他应用程序。

### Activity的生命周期
> 参考文章：[深入理解Activity的生命周期](https://www.jianshu.com/p/fb44584daee3)

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200607214328.png)

方法 | 作用
--|--
`onCreate` | 进行初始化工作，此时**Activity还在后台，不可见** 
`onStart` | 此时Actvity**已经可见**，但是还没出现在前台，**不可交互** 
`onResume` | 此时Activity出现在前台并**可交互** 
`onPause` | 当Activity要跳到另一个Activity或应用正常退出时都会执行这个方法。此时Activity在前台并**可见 
`onStop` | 此时Activity已经**不可见**了，（但是Activity对象还在内存中，没有被销毁） 
`onDestroy` | 这个阶段Activity被销毁 
`onRestart` | restart表示重新开始，Activity在这时**可见**，当用户按Home键切换到桌面后又切回来或者从后一个Activity切回前一个Activity就会触发这个方法。这里一般不做什么操作。 

### Activity的四个启动方法
> 给👴整懵逼了，看都看不懂

### Fragment的生命周期

方法 | 作用
--|--
`onAttach()` | Fragment和Activity建立关联的时候调用，被附加到Activity中去。
`onCreate()` | 系统会在创建Fragment时调用此方法。可以初始化一段资源文件等等。
`onCreateView()` | 系统会在Fragment首次绘制其用户界面时调用此方法。 要想为Fragment绘制 UI，从该方法中返回的 View 必须是Fragment布局的根视图。如果Fragment未提供 UI，您可以返回 null。
`onViewCreated()` | 在Fragment被绘制后，调用此方法，可以初始化控件资源。
`onActivityCreated()` | 当onCreate()，onCreateView()，onViewCreated()方法执行完后调用，也就是Activity被渲染绘制出来后。
`onPause()` | 系统将此方法作为用户离开Fragment的第一个信号（但并不总是意味着此Fragment会被销毁）进行调用。 通常可以在此方法内确认在当前用户会话结束后仍然有效的任何更改（因为用户可能不会返回）。
`onDestroyView()` | Fragment中的布局被移除时调用。
`onDetach()` |Fragment和Activity解除关联的时候调用。


### Fragment和Activity的交互

> 交互就是互相传数据嘛


### Fragment的使用场景

- 需要对某个页面进行反复替换（比如）
- 结合 ViewPager 作导航栏，实现导航切换功能
### service的生命周期

## Java

### stringbufffer与stringbuilder

- StringBuffer是线程安全的
- StringBuilder是非线程安全的


## 算法与数据结构


### 怎么判断一个链表是否形成环

## 设计模式

## 计算机网络

### TCP三次握手




