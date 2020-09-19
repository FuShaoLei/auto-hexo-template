---
title: 解决git clone超慢速度的问题
date: 2020-05-28 20:26:06
---

> 思路是用码云进行clone后修改配置文件以对应到github上

<!--more-->

## 一，在gitee中点击

>  首先你得先有个码云账号

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200528203232.png)

## 二，粘贴上原地址

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200528205226.png)

点击导入
## 三，在本地git clone
![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200528205536.png)

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200528205230.png)

看到这个速度，我不禁老泪纵横，果然不一下子，就完成了，不过还有最重要的一步

## 四，关联到github仓库

找到隐藏文件`.git`

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200528205237.png)

进入config里

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200528205242.png)

把url改成原来github仓库的url，然后 就大功告成啦！

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200528205247.png)

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200528210044.png)

## 参考

[直击痛点：一招搞定GitHub开源项目下载加速！](https://www.bilibili.com/video/BV1aE411p7Cd)