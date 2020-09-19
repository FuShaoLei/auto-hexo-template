---
title:  flex布局笔记
date: 2020-04-25 18:10:39
---
> 因为要仿照一个网站做一款hexo主题，发现里边有很多flex布局，自己照葫芦画瓢很是费劲，不如系统学过，反正也不是很费时间。。下面开始

先放参考教程: [30 分钟学会 Flex 布局](https://zhuanlan.zhihu.com/p/25303493)

<!--more-->

## 基础知识

指定布局：

```css
.container{
    display: flex
}
```

> tip: 当设置flex布局后，子元素的float clear verticle-align失效

可以在父container中设置的属性

属性 | 作用 | 详解
--|-- | --
flex-direction| 决定item的排列方向 | row：（默认）水平方向 <br>row-reverse :水平反方向<br>column: 垂直方向<br>column：垂直方向，由下往上排列 
flex-wrap| 决定item是否可换行 | nowrap: (默认)不换行<br>wrap: 超出容器时换行，第一行在最上<br>wrap-reverse 同上，不过第一行在最下 
flex-flow| flex-direction和flex-wrapd的简写形式 | 默认值 row nowrap<br>原作者写道 没有什么卵用，我😂😂 
justify-content| 决定item在主轴的对齐方式 | flex-start : （默认值）左对齐<br>flex-end：右对齐<br>center：居中<br>space-between：两端对齐，间隙相等<br>space-around：类似上面那个属性，不过项目两侧的间隙相等 
align-items| 决定item在交叉轴的对齐方式 | stretch：（默认值）不是很理解。。<br>flex-start：交叉轴起点对齐<br>flex-end：交叉轴的终点对齐<br>center：交叉轴的中点对齐<br>baseline：item的第一行文字的基线对齐 
align-content| 待补充。。我跳着看 |  

> 其实学到flex-wrap那里我的问题已经解决了，但这个布局属性实在是太强大了，我决定继续学下去

可在子item中设置的属性

属性 | 作用 | 详解
--|-- | --
order |定义item在container内的排列顺序 |越小越靠前
flex-basis |分配多余空间，的方法？？ |默认auto


待补充。。