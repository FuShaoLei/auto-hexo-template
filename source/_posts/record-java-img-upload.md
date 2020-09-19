---
title: java打造一个图片上传工具
date: 2020-07-03 12:25:29
tags:
categories:
---

## 前言
hexo博客，图片是个问题，有一种方法是，把图片放在一个文件夹里，和hexo一起部署，然后博客里用相对路径来引用，这里有个问题，假如博客迁移，或者想转平台发布的时候，每次图片都要找出来然后再贴上去，这真是大大的不便啊。还好后来发现了picgo这个软件，做为资深白嫖党，**picgo+github+jsDelivr**的组合做图床简直香的不要不要的，但是，我发现，用picgo来上传图片到github并不稳定，然后我又是个急性子，有时候想上传一张图片的时候给我报错，我特么能忍吗，所以想自己动手丰衣足食

## 尝试一：调用github api
> 原因是昨天玩travelling 的时候看见了这篇文章：[Java调用Github API实现上传文件到Github仓库](https://fx7.top/index.php/archives/91/)

心血来潮，跟着作者写demo，不过弄完了我发现，调用github api这种方法上传简单txt文件的没问题的，上传图片之类的问题就大了，因为`content`要求的是`base64`格式嘛，然后图片的`base64`格式出来的字符串就长的不行，每次都失败（回传了个422错误码），无语，然后 我还发现，这东西还特么的不稳定，有时候会`connection reset`链接错误，看到这个时我才明白，为什么picgo上传到gihub会不稳定，也可能是我网的问题，我问Hexo群里，都是蛮稳定的，不知道为什么我这个很不稳定

第一次尝试 失败

## 尝试二：Jgit
`Jgit`是一个由Eclipse基金会开发、用于操作git的纯Java库。（也就是可以用java进行`git add .`，`git commit -m "update"`等操作）于是我搜这搜那，终于在今天的上午写成了一个demo，完美实现了`git add .`,`git commit -m "update"`，`git push`三连。不过这样还不够，少了一些b格，然后就琢磨着怎么搞一个界面出来，于是接触道理swing，反正啥也不哦那个，就东拼拼，西凑凑，弄了一个东西出来，可以实现拖拽上传，成果如下

![](https://cdn.jsdelivr.net/gh/fushaolei/ImagitcTest/test.gif)

完美实现上传！在这里要特别感谢测试工具人——[策酱](https://www.cnblogs.com/occlive/)

此项目的github地址：https://github.com/FuShaoLei/Imagic
虽然界面是有些丑啦，但是用起来可比picgo流畅多了，没出现过什么卡顿现象

第二次尝试 成功了^^

> 补充一下思路啊，就是拖拽图片后获取绝对路径，根据绝对路径来复制到本地的git仓库，然后再git三连到远程仓库，然后组合连接返回就好
### 畅想
未来准备给Imagic加上更多的功能，因为我的定位就是专门为github上传图片的，然后可以返回一个自动组成的jsDelivr加速链接，也打算用Swing开发，不用javaFX了（也会考虑）
先列举一些以后要添加的功能

- 图片管理（复制链接，删除图片，修改图片名，批量删除，批量添加等）
- 自带截图（我一般都是用的qq截图，这样太麻烦了，每次截图都要打开qq，多low啊）
- 自带录取gif图（打算参考参考greenTogif的源码）

