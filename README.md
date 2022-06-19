# 2022年6月19日更新
现在不知道什么情况不好用了

## 使用步骤

### 一，import这个仓库

点击新建一个仓库，你会在新建仓库页面看到这个`Import a repository`，点它

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200921213026.png)

然后你会看到如下图的内容

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200921213146.png)

在`You old repository's clone URL`下填我这个项目的链接

```html
https://github.com/FuShaoLei/auto-hexo-template
```

然后为了安全起见（或者说是为了隐私起见），将仓库设为`private`

都设置完后点击下面那个绿色按钮`Begin import`即可

完成时如下

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200921213520.png)

### 二，根据你的情况修改参数

要配置的有

- 配置公钥和私钥
- `.github/workflows/main.yml`里的用户名和邮箱
- `_config.yml`里的`root`和`deploy`

下面一一说明

#### a.配置公钥和私钥

在你的本地`ctrl+r`输入`cmd`调出小黑块，输入

```
ssh-keygen -t rsa -C "<你的github邮箱>"
```

然后在`C:\Users\用户名\.ssh`中可找到

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200920221956.png)

- 公钥的配置（正常来说应该是配置过了），直接在这个[链接](https://github.com/settings/keys)点击那个new SSH key就可配置
- 私钥的配置，点击 https://github.com/<你的用户名>/<存放源文件的仓库名>/settings/secrets，新建私钥，注意，这里的名称要填`HEXO_DEPLOY_PRIVATE_KEY`

#### b.配置`.github/workflows/main.yml`里的用户名和邮箱

这个不多说了，底部可以找到

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200921214724.png)

#### c.配置`_config.yml`里的`root`和`deploy`

如果你部署的仓库名是`<你的github用户名>.github.io`），那么用默认的就行了，如果不是的话，要改成

```yml
root: /<仓库名>/
```

然后是`deploy`，大家根据自己的需求来改就好了

```yml
deploy:
  type: git
  repository: git@github.com:<你的用户名>/<部署hexo的仓库名>.git
  branch: master
```

### 三，允许使用github aciton即可

![](https://cdn.jsdelivr.net/gh/fushaolei/img2/20200921215108.png)

点击那个绿色的按钮即可
