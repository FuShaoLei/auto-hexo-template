---
title: IDEA食用小记
date: 2020-06-14 21:36:08
---

> 哭唧唧，用惯了eclispe的我用起idea就像一个傻子，现在记录一下，以免忘记
> 所用版本：idea 2020.1


## 1. 下载和安装
去官网下载：https://www.jetbrains.com/idea/download/
安装随意，破解的话 看这篇[文章](https://nymane.github.io/post/2020-04-14-IntelliJ_IDEA_2020.1%E6%B3%A8%E5%86%8C%E7%A0%81%EF%BC%88%E4%BA%B2%E6%B5%8B%E6%9C%89%E6%95%88%EF%BC%8C%E5%8F%AF%E6%BF%80%E6%B4%BB%E8%87%B3_2089_%E5%B9%B4)

## 2. 配置maven
> maven的作用就是帮助我们下载需要的jar包，不需要在自己去网上找来找去了

去这个页面:
![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200614230817.png)

然后解压，记住你解压后的位置，比如我直接解压到E盘
然后是配置环境，电脑>属性>高级系统设置>环境变量，在系统变量中添加一个变量为`M2_HOME`，值为你的maven存放路径，然后到path里添加一个maven的bin路径，懒了不贴图了 
在cmd中输入`mvn -v`出现maven的版本号 ，就说明配置成功啦！

这时还没完：
进入`E:\apache-maven-3.6.3\conf`路径下。打开setting.xml
在mirrors中添加一个镜像
```xml
     <mirror>
            <id>nexus-aliyun</id>
            <mirrorOf>central</mirrorOf>
            <name>Nexus aliyun</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    </mirror>
```
阿里云镜像，到时候下载jar包时会更快

> 下载的路径还没修改，将在后续补上

## 3. Idea配置maven
先随意创建一个项目。。。进去后
![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200614233119.png)
![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200614233133.png)
![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200614233140.png)

```
-Xms1024m -Xmx2048m
```
好了 这样后，每创建一个新的项目，都会自动给你配置maven的路径，然后下载jar包的速度也会相应的加快，这给我们的开发带来了极大的便利

## 4.其他
### 常用快捷键

- `tab` 将选中的代码块整体右移，`tab`+`shift`整体左移
- `alt`+`insert` 有多个选项，有getter setter方法，还有构造等等
- `alt`+`enter`自动补全（？）