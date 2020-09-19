---
title: Linux笔记
date: 2020-07-13 00:17:53
tags:
categories:
---
> 参考资料: [Linux常用命令](https://blog.csdn.net/qq_23329167/article/details/83856430?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase)

## 基础
### 关机/重启
- 关机：`shutdown -h now`
- 重启：`shutdown -r now`

### 帮助
例如想查看`shutdown`命令的用法，可以这样
```
shutdown --help
```
就会出现：
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200713005842.png)

更详细的，输入这个
```
man shutdown
```
就会出现
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200713005909.png)

按q可退出

### 目录切换
cd 后面更不一样的东西会有不一样的效果

命令 | 切换到
--|--
`cd /` | 切换到根目录
`cd /user` | 切换到更目录下的user目录
`cd ..` | 切换到上一级
`cd ~` | 切换到home目录
`cd -` | 切换到上次回访的目录（？）

### 目录查看

命令 | 查看..
--|--
`ls` |  查看当前目录下的所有目录和文件
`ls -a` | 查看当前目录下的所有目录和文件（包括隐藏的文件）
`ls -l 或 ll` | 列表查看当前目录下的所有目录和文件（列表查看，显示更多信息）
`ls /dir` |  查看指定目录下的所有目录和文件   如：ls /usr

## 目录操作

### 增 mkdir
命令 | 作用
-- |--
`mkdir    aaa`     | 在当前目录下创建一个名为aaa的目录
`mkdir    /usr/aaa`  |  在指定目录下创建一个名为aaa的目录

### 删 rm
删除文件：
`rm 文件`        删除当前目录下的文件
`rm -f 文件`    删除当前目录的的文件（不询问）

删除目录：
`rm -r aaa`    递归删除当前目录下的aaa目录
`rm -rf aaa`    递归删除当前目录下的aaa目录（不询问）

全部删除：
`rm -rf *`    将当前目录下的所有目录和文件全部删除
`rm -rf /*`    【自杀命令！慎用！慎用！慎用！】将根目录下的所有文件全部删除

注意：rm不仅可以删除目录，也可以删除其他文件或压缩包，为了方便大家的记忆，无论删除任何目录或文件，都直接使用 rm -rf 目录/文件/压缩包

### 改 mv cp

#### 一、重命名目录
命令：`mv 当前目录`  新目录
例如：`mv aaa bbb`    将目录aaa改为bbb
注意：mv的语法不仅可以对目录进行重命名而且也可以对各种文件，压缩包等进行    重命名的操作
#### 二、剪切目录
命令：`mv 目录名称 目录的新位置`
示例：将/usr/tmp目录下的aaa目录剪切到 /usr目录下面     mv /usr/tmp/aaa /usr
注意：mv语法不仅可以对目录进行剪切操作，对文件和压缩包等都可执行剪切操作
#### 三、拷贝目录
命令：`cp -r 目录名称 目录拷贝的目标位置`   -r代表递归
示例：将/usr/tmp目录下的aaa目录复制到 /usr目录下面     cp /usr/tmp/aaa  /usr
注意：cp命令不仅可以拷贝目录还可以拷贝文件，压缩包等，拷贝文件和压缩包时不    用写-r递归

### 查
命令：find 目录 参数 文件名称
示例：`find /usr/tmp -name 'a*'`    查找/usr/tmp目录下的所有以a开头的目录或文件

> 这里这块直接复制粘贴了的，感觉作用不是很大
> 懒了，这东西好繁杂