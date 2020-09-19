---
title: Hexo博客备份过程记录
date: 2020-05-31 11:18:27
---

> 小记录

<!--more-->

## 备份实质

由于我主题文件已经备份到github： https://github.com/FuShaoLei/hexo-theme-volantis （当然是fork了大佬的）

贴一个原作者地址：https://github.com/xaoxuu/hexo-theme-volantis

主题已经备份了，那么其他要备份的也就是这一部分了

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200531114624.png)

**即全部md文件 **

然后还要知道github pages的机制，如果你的仓库名是 `<username>.github.io`的话，pages服务默认在master分支，否则会默认在`gh-pages`分支上
这有就是为什么在配置博客的`config.yml`的时候，branch要填master的原因
![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200531124128.png)

好了，有了以上认识后，我们就可以开始备份我们的博文了，（其实就简单的把本地仓库关联到远程仓库罢了）



## 开始操作

### 一，新建分支

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200531124705.png)
并设为**默认**（**这一步是方便我们在push的时候，不用指定分支什么的了**）

点击setting

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200531124709.png)

### 二，关联到远程仓库

在`/source`里的`git bash`小黑块里依次输入：

> tips: 在小黑块中复制粘贴使用`shift+ins`

  1. `git init` （初始化）
  2. `git remote add origin git@github.com:FuShaoLei/FuShaoLei.github.io.git`
     为的是关联到远程仓库
  3. `git pull --rebase origin back-up`为的是和远程仓库同步（因为新建的分支上是原来master里的东西，需要我们删除）
  4. 然后`git switch -c back-up`（新建并跳转到此分支），这个本地分支名一定要与远程仓库那个分支名一样！
  5. 把除了`.git`的文件全删了，然后`git add .` ,`git commit -m "xx"`, `git  push -u origin back-up`，发现远程仓库这个分支里的东西果然全被删了
  6. 将备份的博文放入，然后重复上面的，不过`git push -u origin back-up`可以换成`git push`了

图片待补充。。。。

## 参考资料

[使用hexo，如果换了电脑怎么更新博客？ - 直上云霄的回答 - 知乎](https://www.zhihu.com/question/21193762/answer/489124966)