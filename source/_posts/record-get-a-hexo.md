---
title: 如何创建一个Hexo博客
date: 2020-06-21 00:38:22
---

> 自用教程

## 环境准备
- Node.j：: https://nodejs.org/en/
- Git：https://git-scm.com/
- 一个Github账号：https://github.com/， 并且创建一个名为 <用户名>.github.io的仓库

## 安装Hexo
### 全局安装

```npm
npm install hexo-cli -g
```
或
```npm
npm install -g hexo
```


### 初始化
```npm
hexo init blog  ## 在blog文件夹中初始化hexo
cd blog ## 进入blog文件夹
hexo g  ## 编译
hexo s  ## 本地预览，在浏览器中输入localhost:4000看看效果
```

## 部署到Github Pages
### 配置SSH密钥
在博客文件夹中
```npm
ssh-keygen -t rsa -C "1563250958@qq.com" 
```
然后
```npm
clip < ~/.ssh/id_rsa.pub
```
将公钥的内容复制到系统粘贴板上

在github中，以此`setting`->`SSH and GPG keys`->添加一个新的SSH key（key就填公钥）（可允许`ssh -T git@github.com`测试成功或不成功）

### 配置hexo
复制`<用户名>.github.io`仓库中的ssh链接备用，然后hexo根目录的`_config.yml`这样配置：
```yml
deploy:
  type: git
  repository: git@github.com:FuShaoLei/FuShaoLei.github.io.git
  branch: master
```
然后还要再安装一个东西

```npm
npm install hexo-deployer-git --save
```
到这就大功告成啦~