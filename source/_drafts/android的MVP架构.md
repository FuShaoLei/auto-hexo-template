---
title: android的MVP架构
date: 2020-06-25 16:48:18
---
> 由于之前写的android程序都不在意架构什么的，但前几个星期面试时被问到过，所以现在来学习。在学习android的MVP模式的时候我的思想受到了极大的撞击，脑阔疼QAQ，所以特写一篇博文 备忘

## 释意

### M：Model

模型，数据层，负责对数据的存取操作（例如数据库的读写，网络的数据的请求等）


### V：View

视图层，用于交互

### P：Presenter

连接View层与Model层的桥梁并对业务逻辑进行处理

### 三者关系
![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200626215435.png)

## 具体实现
> 刚刚写了两个例子，稍微有些明白了QAQ，等我再研究研究再写出来，这个真是搞得我脑阔疼


## 参考
- [Android官方MVP架构解读](https://blog.csdn.net/ljd2038/article/details/51477475)
- [Android中用到的MVP模式](https://blog.csdn.net/weixin_28774815/article/details/80960779)
- [Android MVP 十分钟入门！](https://juejin.im/post/58870cc2128fe1006c46e39c#heading-9)
- [浅谈 MVP in Android](https://blog.csdn.net/lmj623565791/article/details/46596109)
