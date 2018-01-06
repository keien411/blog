---
title: git 学习记录（项目初始化跟踪远程仓库）
date: 2016/11/09 20:30:11
categories:
- Technology
- Git
tags:
- Technology
- Git
---
# 前言
好记性不如烂笔头，量变引质变，记录下git学习记录。

<!-- more -->

## 开始
```
首先大家的电脑都安装git了吧，没有就自行google安装，这里就不列出步骤了
```
> 这里先介绍一种情况
### 你已经有一个项目在电脑上，需要git 上传到开源中国仓库
(1). 在项目的目录下git bash
```js
    git init
```
> 这样就有一个git 项目了,这边可以先放着。

(2). 在git开源中国中创建一个项目，如图所示

![git项目创建](http://ogda5d704.bkt.clouddn.com/git.png)

> 复制项目地址

![地址](http://ogda5d704.bkt.clouddn.com/fuzhigit.png)

(3). 在刚才的项目里打开git bash，输入
```js
git remote add origin git@git.oschina.net:XXXXXX.git

```
> origin 后面是你刚才复制的地址
> 可以检查下添加成功了吗    git remote -v

(4). 现在在添加你的忽略文件吧   .gitignore
> 看你心情添不添加，建议最好添加
```js
git add .gitignore
git commit -m'first commit'
```

(5). 最后跟踪远程仓库
```js
git push -u origin master 
```
> 将本地主分支推到远程(如无远程主分支则创建，用于初始化远程仓库)
> 刷新你的开源中国，看下添加成功了吗？
# 最后
```
这里就介绍这一种情况啦，如有错误之处，多谢指出。
上传到github的步骤应该差不多。
```

