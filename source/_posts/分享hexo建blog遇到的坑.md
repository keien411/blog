---
title: 分享hexo建blog遇到的坑
date: 2018/01/01 21:45:11
categories:
- Technology
- Hexo
tags:
- Technology
- Hexo
---

## 前言
元旦放假，对于人潮的恐惧，于是在家搞起了hexo，很久之前就想干的事情了，说干就干，陆陆续续的干了一天，差不多都建好了，还差一个域名解析（域名还在来的路上呢...），基本可以访问，顺便把我万年前写的博客放上去了，嗯，还算有个样子。废话不多说，先看看成果[keien](https://keien411.github.io/)。
<!-- more -->
## 搭建
- 网上应该都有很多教程了，我找了一篇号称最详细的[hexo搭建](http://www.lovebxm.com/2017/05/30/buildBlog/#%E5%8F%91%E8%A1%A8%E4%B8%80%E7%AF%87%E6%96%87%E7%AB%A0),前面的几个步骤都是搭建环境，比如搭建 Node.js 环境，搭建 Git 环境，都是相对比较简单的，我的电脑这些的环境都搭好了，直接跳过。简单提下注意的点
1. 在github上建的仓库名称要是  yourname.github.io , 比如我的名字是keien411,那么仓库名称就是keien411.github.io

> 啊，就是注意这一点就好了。

- 然后就是搭建hexo的环境了，执行命令
``` 	
npm install hexo-cli -g
```
- 接下来依次执行
```
hexo init keien411.github.io
cd keien411.github.io
npm install
hexo server
```
- 不出意外，你用电脑访问 http://localhost:4000 ，就能看到本地的博客搭建好了，接下来就是关联 Hexo 与 GitHub Pages，上面的最详细已经详细介绍了，我在这里提一点
1. 设置SSH密钥的时候不要设置密码

- 这样就差不多成功了！

## 遇到的坑
我发布的文章点击分类和标签是404，解决方案
1. 首先查看你的source下有没有 categories 和 tags 的文件夹，如果没有，执行以下命令
```
hexo new page "tags" 

hexo new page "categories"
```

2. 分别编辑 /tags/index.md 和 /categories/index.md 
```
type: "tags"
layout: "tags"


type: "categories"
layout: "categories"
```
3. 最后重新部署，你就可以点击分类或者标签了
```
hexo clean
hexo g -d
```

## 最后
教程这东西不会面面俱到，还是多看看官方的文档才是最实在的