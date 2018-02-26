---
title: hexo+github搭建个人博客
date: 2018-02-09 23:30:02
permalink: hexo+github
categories: 个人博客
tags: [hexo,github]
description:
---

<img src="http://images2017.cnblogs.com/blog/505159/201802/505159-20180209235504591-549621574.jpg" alt="hexo" style="width:100%" />  

## 前言  
Hexo是一款基于Nodejs的快速、简洁且高效的博客框架。Hexo使用Markdown解析文章，在几秒内，即可利用靓丽的主题生成静态网页；GitHub Pages本用于介绍托管在GitHub的项目，不过由于他的空间免费稳定，用来搭建一个博客再好不过了。基于两者的特点与优势，本文主要介绍了结合Hexo+Github搭建个人博客的详细流程。

<!-- more -->
## 简介

### Hexo
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。  
参考地址： [Hexo官网](https://hexo.io/zh-cn/ "Hexo")

### Nodejs
简单的说，Nodejs就是运行在服务端的JavaScript。 基于V8引擎，是目前速度最快的Javascript引擎。chrome浏览器就基于V8，同时打开20-30个网页都很流畅。Nodejs标准的web开发框架Express，可以帮助我们迅速建立web站点，比起PHP的开发效率更高，而且学习曲线更低。非常适合小型网站，个性化网站，我们自己的Geek网站！！  
参考地址： [NodeJs官网](http://nodejs.cn/ "NodeJs")

### Git
Git是一个开源的分布式版本控制系统，用以有效、高速的处理从很小到非常大的项目版本管理。  
参考地址： [Git官网](https://git-scm.com/ "Git")

### GitHub
GitHub是基于Git的一个代码托管平台。开发者可以将代码在 GitHub 上开源，可以浏览其它项目的代码，fork 到自己名下做修改，clone 回本地（没有访问权限的 private repo 除外）使用，也可以发起 pull request 向上游提交自己的修改。  
参考地址： [GitHub官网](https://github.com/ "GitHub")

### GitHub Pages
GitHub Pages本用于介绍托管在GitHub的项目，不过，由于他的空间免费稳定，用来做搭建一个博客再好不过了。每个帐号只能有一个仓库来存放个人主页，而且仓库的名字必须是username/username.github.io，这是特殊的命名约定。你可以通过http://username.github.io 来访问你的个人主页。这里特别提醒一下，需要注意的个人主页的网站内容是在master分支下的。  
参考地址： [GitHub Pages官网](https://pages.github.com/ "GitHub Pages")

### Markdown 
Markdown是一种轻量级的标记语言，它的优点很多，目前也被越来越多的写作爱好者，撰稿者广泛使用。看到这里请不要被**标记**、**语言**所迷惑，Markdown的语法十分简单。常用的标记符号也不超过十个，这种相对于更为复杂的HTML 标记语言来说，Markdown 可谓是十分轻量的，学习成本也不需要太多，且一旦熟悉这种语法规则，会有一劳永逸的效果。  
参考地址： [Markdown语法介绍](https://www.appinn.com/markdown/ "Markdown")

## 搭建流程

### 安装Git和Nodejs
安装Git和Nodejs的过程非常简单，下载好安装包之后，默认安装即可，并且安装完成后会自动将安装路径添加到环境变量中；查看是否安装成功，可以在命令窗口（cmd）中，输入git -version和node -v来验证。  
Git下载地址： [下载Git](https://git-scm.com/download/ "Download Git")  
Nodejs下载地址： [下载Nodejs](http://nodejs.cn/download/ "Download Nodejs")

### SSH授权
在管理Git项目上，很多时候都是直接使用https url克隆到本地，当然也有使用SSH url克隆到本地。这两种方式的主要区别在于：使用https url克隆对初学者来说会比较方便，复制https url然后到git Bash里面直接用clone命令克隆到本地就好了，但是每次fetch和push代码都需要输入账号和密码，这也是https方式的麻烦之处；而使用SSH url克隆却需要在克隆之前先配置和添加好SSH key，因此，如果你想要使用SSH url克隆的话，你必须是这个项目的拥有者。否则你是无法添加SSH key的，另外ssh默认是每次fetch和push代码都不需要输入账号和密码。  
第一步，打开git bash，输入ssh-keygen -t rsa，接着回车三下，然后就会在C盘用户目录下生成id_rsa和id_rsa.pub这两个文件，前者是密钥，后者是公钥。  
第二步，用记事本打开id_rsa.pub，复制其中的全部内容，添加到GitHub上，这样本地的id_rsa密钥就可以和GitHub上的id_rsa.pub公钥进行配对，授权成功，如下图所示：  
![SSH](https://images2018.cnblogs.com/blog/505159/201802/505159-20180225230628646-2135841151.png)  
第三步，SSH key添加之后，就可以在本机git bash中进行测试，输入ssh -T git@github.com进行测试，返回Hi username！You've successfully ......说明你已经成功啦！

### 创建仓库、设置GitHub pages
首先，登录Github，创建一个仓库，因为Github Pages的Repository名字是特定的，所以仓库命名为“用户名.github.io”，比如我的Github的用户名为Harderqian，那么Github Pages的Repository名字就是Harderqian.github.io，具体操作如下图所示：  
![GitHub Pages](https://images2018.cnblogs.com/blog/505159/201802/505159-20180225224500229-419892135.png)  
然后，进入仓库的Setting界面，设置GitHub Pages，具体操作如下图所示：  
![GitHub Pages](https://images2018.cnblogs.com/blog/505159/201802/505159-20180225224918110-1921817732.png)  
如果用户名.github.io（或者第三方域名）可以正常访问了，那么表示GitHub pages的配置正确无误。

### 安装Hexo
在计算机的磁盘中创建一个目录，例如D:/hexo，然后在命令行中进入该目录。  
第一步，安装hexo，输入如下命令：

``` bash
npm install -g hexo-cli
```

第二步，初始化hexo，输入如下命令：

``` bash
hexo init  # hexo会在目标文件夹建立网站所需要的所有文件
npm install  # 安装依赖包
```

第三步，有了必要的各种配置文件之后就可以在本地预览效果了，输入如下命令：

``` bash
hexo g # 等同于hexo generate，生成静态文件到public文件夹
hexo s # 等同于hexo server，在本地服务器运行
```
### 关联Hexo和Github Pages
第一步，进入刚刚创建的hexo文件夹，打开站点配置文件_config.yml，在文件底部修改repository内容为之前创建的仓库地址，如下图所示：  
![Hexo](https://images2018.cnblogs.com/blog/505159/201802/505159-20180226213812934-1854966596.png)  
第二步，安装Git部署插件，命令行界面中进入hexo文件夹，输入如下命令：

``` bash
npm install hexo-deployer-git --save
```

第三步，回到命令行界面，执行如下命令：

``` bash
hexo clean # 作用为清除静态文件夹的内容并删掉，主要用于更改变更了某些地方导致页面显示不完善  
hexo g
hexo d # 等同于hexo deploy，部署到服务器（github）
```

第四步，现在，试试在浏览器的地址栏中输入： “你的用户名.github.io”，此时，出现Hexo的Hello world界面，表明关联成功了。