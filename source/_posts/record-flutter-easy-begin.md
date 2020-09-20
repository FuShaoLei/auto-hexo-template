---
title: Flutter快速入门
date: 2020-07-17 15:23:41
tags:
---
> 刚开始知道Flutter还是在19年初的时候（？），在学校举办的google开发者大会上知道的，起初也想试试来着，不过他说要按什么环境，我就觉得麻烦就不弄了，直到上次面试威视的时候面试官提及，才想起有这么一个东西，而这时的我已经经历了好多次重装系统（TAT），已经无所畏惧了，程序员嘛，要敢于折腾

## 简介

略

## 配置环境

### 配置`Flutter`环境
看官方这篇教程就好：[入门: 在Windows上搭建Flutter开发环境](https://flutterchina.club/setup-windows/)

列几个点吧：

1. 下载安装包： https://flutter.dev/docs/development/tools/sdk/releases#windows
2. 解压
3. 配置环境变量，在用户变量里加入`flutter/bin`的路径

然后测试一下，win+R 输入cmd启动小黑块 输入`flutter doctor` 出现类似如下 说明成功啦！（存疑）

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200717155819.png)

### 安装`Android studio`插件
需要安装Flutter插件和Dart插件
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200717165537.png)


在安装Flutter插件的时候给我报了个错误：
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200717161918.png)
然后我重启android studio又给我报了一个错误
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200717165419.png)

我特喵 (╯‵□′)╯︵┻━┻

后来重启电脑和连手机热点就解决了。。网速真是个大问题啊

两个插件都安装成功后重启你的android studio就可以看到新增的东西了

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200717165638.png)

## 第一个Flutter程序

最开始也得配置一下flutter的路径
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200717172040.png)

等待创建
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200717172121.png)
这一步我等了有二十分钟...

然后就创建完成啦

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200717172240.png)

运行到手机上看看

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200717173912.jpg)

如果出现这个页面（默认的） ，就说明 我们大功告成啦~~
