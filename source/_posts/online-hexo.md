---
title: github action + hexo 实现在线写博客
---

## 零，前言 

[hexo](https://hexo.io/) 是一款快速、简洁且高效的静态博客框架，因为它的高可定制性，所以深受各个程序员的喜爱，我也曾一头扎进去研究过，先后开发了white和hiya主题，在使用过程中，也渐渐的发现了一些问题

 情景一，当浏览自己某篇博客时发现了一些错误之后想要马上修改时，将要经历经历一下步骤
 1. 在本地的hexo博客文件夹中找到`source/_post`文件夹
 2. 找到那个md文件，打开
 3. 修改
 4. 然后还要经历`hexo clean`,`hexo g`，`hexo d`

情景二，当想要马上写一篇博客时，需要经历以下步骤

1. 在博客根目录中`hexo n "博客名"`
2. 点击进入`source/_post`文件夹中找到这个md文件并打开
3. 写博客
4. 然后还要经历`hexo clean`,`hexo g`，`hexo d`三连



以上过程想必使用过hexo博客的人都经历过吧？不知道你们什么感觉，反正这对于我这种急性子的人来说简直是忍不了(╯‵□′)╯︵┻━┻，而且每次写完博客啊，修改完博客啊之类的，还必须经历过`hexo clean`,`hexo g`，`hexo d`才可以将博客推送到网上去，这玩意我一开始还有耐心，现在就不行了(ノ｀Д)ノ，幸好后来发现了github action可以实现自动部署，再结合自己以往开发hexo主题的经验，做出来了可以在线新建博客或者修改博客的功能（具体可参观我的[博客](https://fushaolei.github.io/)），效果如下：

 新建文章

 ![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200920220049.gif)

 修改文章

 ![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200920220327.gif)

 就这样，利用github action交给github去做`hexo clean`,`hexo g`，`hexo d`三连，很方便的实现了新建文章和修改文章，即优雅，又方便，那么这又是如何做到的呢？下面我将分为两个部分来说明，第一部分是如何结合github action来实现自动部署，第二部分是如何点击某个按钮后进入新建文章页，和修改文章页。

## 一，使用github aciton实现自动部署

1.**在github新建一个仓库，专门用来存放源文件**，我的源文件如下，供各位参考

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200920221609.png)

> 什么？你不会要先git clone到本地后，再将源文件复制粘贴到里面再上传吧？这也太low太笨拙了吧哈哈哈，咳咳，如果你不会将本地仓库关联到远程仓库的话，请按下边步骤进行
>
> 1. 在hexo源文件夹中 `hexo init ` 进行初始化
> 2. 关联远程仓库 `git remote add origin git@github.com:<你的用户名>/<存放源文件的仓库名>.git`
> 3. `git pull --rebase origin master`和远程仓库进行一个同步
> 4. 然后依次进行`git add .`，`git commit -m "init repo"`，`git push -u origin master` ，然后就大功告成啦
>
> 上传好的源文件在github中如下
>
> ![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200921000040.png)

**注意：如theme文件夹中主题文件中有`.git文件`，请将其删除在上传**

2.添加私钥和公钥

在`C:\Users\用户名\.ssh`中可找到

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200920221956.png)



- 公钥的配置（正常来说应该是配置过了），直接在这个[链接](https://github.com/settings/keys)点击那个new SSH key就可配置
- 私钥的配置，点击 https://github.com/<你的用户名>/<存放源文件的仓库名>/settings/secrets，新建私钥，注意，这里的名称要填`HEXO_DEPLOY_PRIVATE_KEY`

3.添加github action

![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200920224635.png)

将以下的代码复制粘贴

```yml
# workflow name
name: Hexo Blog CI

# master branch on push, auto run
on: 
  push:
    branches:
      - master
      
jobs:
  build: 
    runs-on: ubuntu-latest 
        
    steps:
    # check it to your workflow can access it
    # from: https://github.com/actions/checkout
    - name: Checkout Repository master branch
      uses: actions/checkout@master 
      
    # from: https://github.com/actions/setup-node  
    - name: Setup Node.js 12.x 
      uses: actions/setup-node@master
      with:
        node-version: "12.x"
    
    - name: Setup Hexo Dependencies
      run: |
        npm install hexo-cli -g
        npm install
    
    - name: Setup Deploy Private Key
      env:
        HEXO_DEPLOY_PRIVATE_KEY: ${{ secrets.HEXO_DEPLOY_PRIVATE_KEY }}
      run: |
        mkdir -p ~/.ssh/
        echo "$HEXO_DEPLOY_PRIVATE_KEY" > ~/.ssh/id_rsa 
        chmod 600 ~/.ssh/id_rsa
        ssh-keyscan github.com >> ~/.ssh/known_hosts
        
    - name: Setup Git Infomation
      run: | 
        git config --global user.name '<你的用户名>' 
        git config --global user.email '<你登录的email>'
    - name: Deploy Hexo 
      run: |
        hexo clean
        hexo generate 
        hexo deploy
```

**仔细看这段代码，里边要填上你的用户名和邮箱**

DONE!大功告成啦，到这里可以去测试一下，修改修改某个文章标题，看看是否有效果

好了，利用GitHub action实现自动部署这一步已经完成了

## 二，设置点击进入新建或编辑

> 如果你是一名hexo主题开发者的话，这一步对你来说就是无比的简单了，如果你是一名小白的话 也没关系，跟着我的步骤，稍微有些耐心，应该不是什么问题

#### 新建文章

其实完成了第一步，这一步就捉襟见肘了，无非就是点击一个按钮后跳转到**存放hexo源文件仓库的`source/_posts`路径的新建页面**，比如我，链接就是 https://github.com/FuShaoLei/auto-blog/new/master/source/_posts ，效果如下

 ![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200920220049.gif)

放一个模板： `https://github.com/<你的用户名>/<存放博客源文件的仓库名>/new/master/source/_posts`

就是一个链接而已，你可以把它放在menu中，或者任何你想放的地方

### 修改文章

**修改文章本质就是修改源文件中的`source/_posts`目录下的md文件**

而这个md是与path路径有关的，不过一般文章的path路径都类似`/2020/08/09/doc-white/`这样的，有一个日期的前缀，而且有一个斜杠，所以一般要经历以下步骤，

1. 去除这个post的path路径中的数字和斜杠
2. 加上前缀`https://github.com/<你的用户名>/<存放源文件的仓库名>/edit/master/source/_posts/`
3. 加上后缀`.md`
4. 组合成类似`https://github.com/<你的用户名>/<存放源文件的仓库名>/edit/master/source/_posts/<文章名>.md` 的链接即可

下面以`ejs`举例（在`post.ejs`中）

```ejs

<%
<!-- 这个js函数是抄的，见笑 -->
function trimNumber(str){
    return str.replace(/\d+/g,'').replace(/\//g,'');
}
%>
<article id="post">
  <h1><%= page.title%></h1>
  <%-page.content%>
  <a  href="https://github.com/FuShaoLei/auto-blog/edit/master/source/_posts/<%=trimNumber(page.path)%>.md">Edit Post</a>
</article>

```

好了，之后点击那个新增的超链接后 就会跳转到你想要修改的文章了，效果如下

 ![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200920220327.gif)



这样一来，当你新增或修改文章并点击那个`git commit`后，都会出发github action，然后它就会帮你进行hexo三连，也就是自动部署啦



## 参考文章

- [利用GitHub+Actions自动部署Hexo博客](https://blog.csdn.net/u012208219/article/details/106883054?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522160061139819195188346686%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=160061139819195188346686&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v3~pc_rank_v3-1-106883054.pc_ecpm_v3_pc_rank_v3&utm_term=github+action+%E8%87%AA%E5%8A%A8%E9%83%A8%E7%BD%B2hexo&spm=1018.2118.3001.4187)

