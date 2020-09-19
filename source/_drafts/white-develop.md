---
title: white主题开发（更新ing）
date: 2020-07-18 15:48:55
toc: false
---


## 前言
入坑Hexo博客是在2019年的四月份，当时跟着一个up主弄的，弄了好久，用的next主题，也就那个b样，也没写几篇文章，都是一些吐槽之类的东西，然后就遗弃了，后来今年一月份又重新拾起来，先后用了icarus，maupassant，fluid，volantis等主题，后因为喜爱而入了hexo主题的坑，先后开发了glow，anyway，hiya等主题，white主题是今年六月份根据[Typora的更新文档](http://support.typora.io/) 来进行一致的，并且我准备一直做下去，因此，特开一篇博文来记录记录
> 另外想说一下为什么使用hexo博客，因为可定制性高，每一篇博文都是一个md文件，备份方便

## 初衷
因为我不喜欢花里胡哨的东西，也不喜欢在写博客的时候，还要选个图片，选个摘要的地方啊，我觉得这些都是很麻烦的，也没必要，然后我又有严重的对称强迫症，没错，我只喜欢居中的，不喜欢非对称布局的🙃。

## 更新日记

### 2020/07/19
> 开始重写

心乱如麻，先列几个其他网页我喜欢的地方

#### 1. 少数派

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200719104706.png)

内容部分居中设计，而且整体也是有一个一定的宽度，不像我这个一样，有些分散，我这样显得很。。我也不知道怎么形容，反正这点得改，搞得窄一些

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200719105718.png)

少数派这个toc也值得我参考，但是他是单个显示的，而不是整体显示的，这我感觉就不太行了，我觉得这个toc起到的是一个目录的作用，应该是全部显示的

#### 2.[迷你日志](https://minirizhi.com/)
在一个友链的友链上找到的博客，这样的设计就显得蛮紧凑的，我挺喜欢，迷你日志的宽度给我的感觉最舒服
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200719110302.png)

类似的设计还有hugo的主题[zozo](https://themes.gohugo.io/theme/hugo-theme-zozo/)
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200719110515.png)

还有Gridea的主题[Rocky](https://gridea-theme-rocky.netlify.app/)
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200719110652.png)

（其中这个Gridea这个主题给我的印象蛮深的，尤其是那个封面图，我记得是封面图在最上的，不知道怎么现在变成这样）

无一例外，他们的特点都是将整体缩小到一定宽度中。而我的确实有些分散了QAQ，然后前面也说过了，我懒的在写博客的时候配上首图或者写摘要。这是一点，其实再要可以用自动截断来代替，但自动截断有时候截的地方有些奇怪，所以首页显示文章的话只会出现文章的**标题**，还有可能会有时间等等。

刚刚逛[Dribbble](https://dribbble.com/shots/4950641-Portfolio-3-0)的时候又发现一个和我很相似（其实我和人家相似啦）的风格，或许可以借鉴一下
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200719163222.png)

（其实有时候我挺矛盾的，有时候喜欢安安静静很简约的风格，有时候喜欢花里胡哨的风格，也许是我人格分裂了吧இ௰இ）

布局有些思路了，接下来是颜色啦
因为主题名叫white，所以背景颜色就是#fff啦，以后也会加入暗黑模式什么的吧，然后文字的颜色也就#333，再加一个辅色，选什么色好呢，算了先这两种色吧233

总结一下今天的思考

布局方面：

- 全局限制在一个宽度
- 博文陈列时只显示标题，或者再加上时间 等等

配色：

- 背景：#fff
- 字体：#333

经过一翻努力，做出了首页的样子

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200719221619.png)

果然和我想的一样，这样的布局就是比以前紧凑了些，现在得考虑，文章展示放在上面地方了...，因为我的文章嘛，上面也说了，懒的招封面首图，懒得加摘要，不过这不能一概而论，要分情况，有时候嘛，超级想写一些字的时候，就不想弄首图了，也懒的写摘要了，就想发布，有时候嘛，想美美的，精致的写一篇博客（这种情况偏少）。程序员嘛，写的都是写技术文章，配不了几张图。



### 2020/07/20
今天还是一如既往的没思路 ，我一个搞Android的，却来碰这玩意，譬如使惯了刀，这回要我耍剑，能行么？可愈陷愈深，无法自拔，事实证明，写代码是会上瘾的。今天也先看看别人是怎么写的吧
#### Raditian Free Hugo Theme
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200719230713.png)
OMG! 这个和我的布局简直相差无几，但是也仅仅是这里相同而已，往下我并没有看到我期待的样式，这是一个有点像简历的形式

#### Codex

再看看这个

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200719232102.png)
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200719232122.png)
OMG OMG oh my fucking god. 居然和我以前的设计一模一样（事实是我借鉴了他的首页设计哈哈哈）

其实今天还在考虑是不是要全部有首图的样式，这样至少可以花哨一些，不至于那么简洁。然后再逛dribbble的时候看到这个作品

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200720112930.png)

Jobs下的设计马上让我联想到了hexo的主题[Clover](https://github.com/esappear/hexo-theme-clover),如下。

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200720113059.png)

### 2020/07/21
大概的样子已经弄出来了！
- 旧版首页
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200721085754.png)
- 新版首页
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200721085822.png)
- 旧版archive页
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200721090105.png)
- 新版archive页
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200721090155.png)
- 旧版post页
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200721090223.png)
- 新版post页
![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200721090240.png)

可以明显感觉到，新版的页面更加紧凑了，另外 我加入了一个鲜艳的色调，还有动画，使得这个white看起来不太white。

加入了valine评论和gitalk评论系统

valine好处是不用登录都可以评论，但是会有人打广告QAQ
gitalk的话必须有github账号才可以使用，提高了门槛，不过文章的链接字符不能超过五十个字符。。这就需要用英文来命名md文件了，不过稍微学习（翻译）一下不是问题（面露难色），这两者我偏向于gitalk，因为 现在valine的邮件回复没有了，gitalk还可以提醒你

## 参考

本主题在开发过程中或多或少的借鉴前人的一些作品

- [Typora的更新文档](http://support.typora.io/)：我见过很多简约的主题，但是没见过如此简约的主题，再配上好看的字体，简直了，那一刻开始我就马上找到了它的源码，并下手开发hexo版的主题
- [TMaize Blog](https://blog.tmaize.net/)：同样也是简约布局，但是它的归档页是分类的，就是分类名后面跟着文章，再加上之前入坑就是因为想要自己弄一个可以分类后跟文章名的主题，所以就用上了
- [群狼动力](https://volf.club/)：travelling的发起者，原模版是html5up上的，这是我首页的启发（其实我就是照搬的，不过没有抄代码嘻嘻嘻）
- [Geekplux](https://geekplux.com/)：借鉴了他那个好看的hover