---
title: Hexo写作技巧
date: 2018-03-11 18:31:05
permalink: AboutHexoWriting
categories: 个人博客
tags: Hexo
description:
---

<img src="http://hexorepo.oss-cn-hongkong.aliyuncs.com/images/hexoIndex.jpg" alt="hexo" style="width:100%" />  

## 前言  
构建完博客、配置好主题后，只能说有个漂亮的外壳，内容丰富且颜值高的文章才是真正的精华，本文主要介绍了几个提高文章颜值的技巧方法。

<!-- more -->

## 定制属于自己的文章模板文件
文章模板文件的个性化会直接影响文章（post）的主要布局，文章模板文件位于`\scaffolds\post.md`，根据功能需求和对文章布局的理解，我定制了文章模板文件，如下所示：

```
---
title: {{ title }}
date: {{ date }}
permalink: 
categories: 
tags: 
description:
---

<img src="http://" alt="" style="width:100%" />  

## 前言  

<!-- more --> 
```

>**提示：**自定义permalink，可以避免文章URL中出现中文的情况。

## 定制属于自己的写作样式
用一些特殊的样式，可以增加文章的可读性，下面介绍一下我自己定制的几种样式。

### 自定义文章内超链接样式
在`\themes\next\source\css\_custom\custom.styl`文件中，添加以下代码：

``` css
.post-body p a {
    color: #649ab6;
	border-bottom-color: #649ab6;
}
.post-body p a:hover {
    color: #649ab6;
	border-bottom-color: #649ab6;
	font-weight: bold;
}
```

### 自定义文章内引用块样式
在`\themes\next\source\css\_custom\custom.styl`文件中，添加以下代码：

``` css
blockquote {
    padding: 0 15px;
    color: #666;
    border-left: 4px solid #649ab6;
}
```

### 自定义文章行内代码样式
在`\themes\next\source\css\_custom\custom.styl`文件中，添加以下代码：

``` css
code {
    color: #ff7600;
    background: #fbf7f8;
    margin: 2px;
	border: 1px solid #c1c1c1;
}
```

### 自定义文章内Span样式
在`\themes\next\source\css\_custom\custom.styl`文件中，添加以下代码：

``` css
span#inline-blue,span#inline-green,span#inline-purple,span#inline-yellow {
    display: inline;
    padding: .2em .6em .3em;
    font-size: 90%;
    font-weight: 700;
    line-height: 1;
    color: #fff;
    text-align: center;
    vertical-align: baseline;
    border-radius: 0;
    white-space: nowrap;
}

span#inline-yellow {
    background-color: #f0ad4e;
}

span#inline-green {
    background-color: #5cb85c;
}

span#inline-blue {
    background-color: #2780e3;
}

span#inline-purple {
    background-color: #9954bb;
}
```

## 总结
本文主要介绍了几个Hexo博客写作的小技巧，参考、借鉴了很多优秀的个人博客，文章有不足或者疏漏的地方，欢迎大家在下面评论区讨论。