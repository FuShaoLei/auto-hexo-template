---
title: white主题配置 才怪啦 早就弃坑了
date: 2020-08-09 23:31:29
---

## 👋Hi there

欢迎使用本主题 ，**White** 是一个在个性和极简之间徘徊的主题，（因为作者本身性格就是这样的人，而且搞不好心态爆炸会删库跑路，还请喜欢的各位及时fork🤣

如果你喜欢这款主题的话，不妨给我一个star 感激不尽！

##  安装
> 方便备份和更新

1. fork 本项目
2. `git clone https://github.com/<你的用户名>/hexo-theme-white.git themes/white`
3. 修改根目录下的`_config.yml` 为`theme: white`


## 主题配置

> 其实config文件里写的很明白了，现在就重新列一下，添加一些不必要的说明

### 可自定义style

```yml
############## style ##############
style:
  layout:
    max-width: 1130px #总体宽度
    post-max-width: 800px #文章内容宽度
  color:
    theme-main: "#1A98FF" # 主色调
    theme-secondary: "#DDF0FF" # 次色调
    text-main: "#333333" # 文字主色调
    text-secondary: "#898FA0" # 文字次色调
  animation:
    open: true # 如果开启动画的话会引入animation.css
```

### 主页配置

#### home页和archive可选配置

```yml
# home页可选类型
home:
  type: "img" # 主页的类型，可选 home | img | simple

# archive页可选类型
archive:
  type: "simple" # archive的类型，可选 img | simple
```

type为home就是一个封面，为img就是图片加标题的形式，simple就是极简模式

### 随机cover

当你懒的找封面而又想用img模式的时候，我为你准备了些随机封面

```yml
archive_img_mode:
  default_cover: #默认的cover
    - https://cdn.jsdelivr.net/gh/fushaolei/cdn-white@1.0/cover/01.jpg
    - https://cdn.jsdelivr.net/gh/fushaolei/cdn-white@1.0/cover/02.jpg
    - https://cdn.jsdelivr.net/gh/fushaolei/cdn-white@1.0/cover/03.jpg
    - https://cdn.jsdelivr.net/gh/fushaolei/cdn-white@1.0/cover/04.jpg
    - https://cdn.jsdelivr.net/gh/fushaolei/cdn-white@1.0/cover/05.jpg
    - https://cdn.jsdelivr.net/gh/fushaolei/cdn-white@1.0/cover/06.jpg
```
> 图片均来自于bing的每日图片，版权归图片原作者所有，我只是搬到了自己的仓库方便使用，如果有侵犯到你的权益，请和我联系 ( •̀ ω •́ )y

### 浏览器标签页配置
```yml
# icon
icon:  #标签页图标，这里可填链接
#  header
site_name: white.
```

### menu
```yml
menu:
  HOME: /
  BLOG: /archives
```

### 全局搜索

```yml
## 本地搜索
search:
  open: false # 是否开启
  page: /search # 页面路径（通常命名为search）
```
如果你想使用的话，请先到根目录执行
```npm
npm install hexo-generator-search --save
```
然后新建一个名为search的page

```npm
hexo new page "search"
```

进入这个文件夹，更改它的`index.md`文件，示例如下
```md
---
layout: search
cover: #你还可以自定义cover
---

```
然后将open设置为true即可开启

### 自我介绍
> 当你的home页有用到type home模式的话 请配置此项

```yml
# 自我介绍
intro:
  title: Hi.I'm White.
  sub: 'A [White](https://github.com/FuShaoLei/hexo-theme-white) theme for [Hexo](http://hexo.io/)' # markdown语法
  avator: https://cdn.jsdelivr.net/gh/fushaolei/img/20200524104925.jpg #头像 暂时还没用到
  author: white #所有文章的默认作者
```

### 联系方式

```yml
#联系方式  
#更多图标：https://remixicon.com/
contact:
  Github:
    - https://github.com/FuShaoLei/hexo-theme-white
    - ri-github-line
  Email: 
    - mailto:1563250958@qq.com
    - ri-mail-line
```

格式就是
```yml
名字:
  - 链接
  - 图标 
```
更多图标请到 https://remixicon.com/ 搜寻，感谢此图标项目的开源作者[xiaochunjimmy](https://github.com/xiaochunjimmy)

### 文章toc设置
```yml
# 文章toc索引栏设置
toc:
  open: true # 是否开启
  side: true  # 选择toc的位置，填true的话toc将会显示在文章的侧边，填false的话 toc将出现在文章的开头
  max: 2 #最大深度
  min: 2 #最小深度
```
其中side如果设置为false的话，将会出现在文章的top部分，如果设置为true的话，将会出现在侧边
min设置的是最小深度，max设置的是最大深度，~~如上面配置所示，min为2，说明h2索引是至少要出现的，不会出现h1索引 （ 突然不知道怎么表达，~~ 如果不理解的话建议你试试 😂 

### highlight
代码高亮，想要使用代码高亮，得先把根目录的**`_config.yml`里的highlight的enable置成false**
```yml
# 插件
plugins:
  highlightjs:
    js: https://cdn.jsdelivr.net/gh/highlightjs/cdn-release@9.18.1/build/highlight.min.js
    css: https://cdn.jsdelivr.net/npm/highlight.js@10.1.1/styles/github.css
    # more: https://www.jsdelivr.com/package/npm/highlight.js?path=styles
```
**注：**  hexo 5.0版本此处有bug（2020年8月10日写），就是渲染不出来大括号（`{`和`}`）

这里博主有点懒了，最近事多心烦，就等着hexo官方更新吧 QAQ

### 评论系统

```yml
# 评论系统设置
comments:
  open: false #是否开启评论系统
  system: gitalk #选择评论系统 可选 valine gitalk livere
  # Valine
  valine:
    appid: #Leancloud应用的AppID  这里和下面的要换成你自己的啊QAQ
    appkey: #Leancloud应用的AppKey
    verify: false #验证码
    notify: true #评论回复提醒
    avatar: robohash #评论列表头像样式：''/mm/identicon/monsterid/wavatar/retro/hide
    #头像类型可见： https://valine.js.org/avatar.html
    placeholder: 留下你来过的痕迹~ #评论框占位符
  # Gitalk
  gitalk:
    owner:  #Github 用户名,
    repo:  #储存评论issue的github仓库名
    admin:  #Github 用户名
    clientID:  #`Github Application clientID`
    clientSecret: #`Github Application clientSecret`
  #livere
  livere: # 前往 http://livere.com/ 申请账号
    dataId: city #免费版本city
    dataUid: #安装代码中 data-uid 后面数据
```

这里的话相关教程大家网上搜就好了。这里就不赘诉了 

> 还是写一些gitalk的坑吧，一个是repo这里 写的应该是**仓库名**，而不是仓库链接或者其他的东西，然后gitalk要上线部署一次才可以，md文件名字最好用英文来命名，如果用中文的话，超出50个字符将会初始化失败
> 

### 其他
```yml
# 页脚
footer: Power by [Hexo](http://hexo.io/) Theme by [White](https://github.com/FuShaoLei/hexo-theme-white) # markdown语法

#有分类时是否开启menu分类页和自定义名字
menu_categories:
  open: true
  name: 分类

#可自定义归档标签页名字 
archive_tab_name: Blog

#图片懒加载
lazyload:
  open: true #是否开启
```
这里就不bb了 大家应该看的懂

## 进阶使用

### 平滑升级

#### 配置
因为主题的更新比较频繁，所以如果你想舒服用到最新的版本的话，就请使用平滑升级

1. 在你**根目录**下的`source`文件夹下新建一个名为`_data`的**文件夹**
2. 复制**主题文件夹**下的`_config.yml`到`_data`文件夹下，重命名为`white.yml`

好了，到这里差不多完成了，以后你需要改动什么，只需要在这个`white.yml`中进行修改(在编译时，会自动将此替换`_config.yml`)

#### 升级
当你看到我的主题有[变更](https://github.com/FuShaoLei/hexo-theme-white/issues/3)时，在主题文件中执行`git pull`拉取最新代码
然后，对比最新主题文件夹下的`_config.yml` 看看有无新增什么东西，添加到你的`white.yml`中即可



