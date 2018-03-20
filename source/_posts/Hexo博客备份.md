---
title: Hexo博客备份
date: 2018-03-19 14:30:58
permalink: AboutHexoBackUp
categories: 个人博客
tags: [Hexo, 备份]
description:
---

<img src="http://hexorepo.oss-cn-hongkong.aliyuncs.com/images/hexoIndex.jpg" alt="hexo" style="width:100%" />  

## 前言  
使用Hexo在GitHub搭建的博客，博客作为一个单独的GitHub仓库存在，但是这个仓库只有生成的静态网页文件，并没有Hexo的源文件，如果要换电脑或者重装系统后，就比较麻烦了，本文主要介绍了一种比较简单的Hexo博客备份方法。

<!-- more -->

## 博客备份
1、创建仓库Username.github.io，如果同名仓库之前已经创建，请将之前的仓库改名，新建的仓库名必须是Username.github.io；  
2、创建两个分支：master和hexo，并设置hexo为默认分支；  
3、将刚刚创建的新仓库clone至本地，将之前的hexo文件夹中的`_config.yml`、`themes\`、`source\`、`scaffolds\`、`package.json`、`.gitignore`复制至克隆下来的文件夹Username.github.io中；  
4、将`themes\next`（我用的是Next主题）中的.git/删除（.gitignore里面的内容要删掉，并且`themes\next\source\lib`目录下的插件中的.git也要删除），否则无法将主题文件夹push至服务器；  
5、在Username.github.io中执行`npm install`和`npm install hexo-deployer-git`；  
6、执行`git add .`、`git commit -m ""`、`git push origin hexo`来提交hexo网站源文件；  
7、执行`hexo g -d`生成静态网页部署到GitHub中； 
>**提示：**这样一来，Username.github.io仓库就有master分支和hexo分支，分别保存静态网页和源文件。

## 修改同步
在本地对博客修改（包括修改主题样式、发布新文章）后：  
1、依次执行`git add .`、`git commit -m ""`、`git push origin hexo`来提交hexo网站源文件；  
2、执行`hexo g -d`生成静态网页部署到GitHub中；  
即重复备份的第6、第7步，以上两步没有严格的顺序。

## 博客恢复
重装电脑后，或者在其他电脑上想修改博客：  
1、安装Git、Nodejs；  
2、使用git clone命令或者github桌面版，将仓库拷贝至本地；  
3、在文件夹内依次执行以下命令`npm install hexo-cli -g`、`npm install`、`npm install hexo-deployer-git`；

## 附录
这里说明一下，博客备份中的步骤3为什么只需要拷贝6个，而不需要全部：  
1、`_config.yml`，站点的配置文件，需要拷贝；  
2、`themes\`，主题文件夹，需要拷贝；  
3、`source\`，博客文章的md文件，需要拷贝；   
4、`scaffolds\`，文章的模板，需要拷贝；  
5、`package.json`，安装包的名称，需要拷贝；  
6、`.gitignore`，限定在push时哪些文件可以忽略，需要拷贝；  
7、`.git\`，主题和站点目录中都有，标志这是一个git项目，不需要拷贝；  
8、`node_modules\`，安装包目录，在执行`npm install`的时候会重新生成，不需要拷贝；  
9、`public\`，`hexo g`生成的静态网页都存放在改文件夹里，不需要拷贝；  
10、`.deploy_git\`，`hexo d`会生成，不需要拷贝；
11、`db.json`，不需要拷贝；
>**提示：**其实不需要拷贝的文件正是.gitignore文件中所忽略的。

## 总结
本文主要介绍了一种比较简单的Hexo博客备份方法，参考、借鉴了很多优秀的个人博客，文章有不足或者疏漏的地方，欢迎大家在下面评论区讨论。