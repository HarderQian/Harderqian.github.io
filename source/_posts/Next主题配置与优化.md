---
title: Next主题配置与优化
date: 2018-03-04 14:24:59
permalink: AboutNext
categories: 个人博客
tags: [Hexo, Next]
description:
---

<img src="http://hexorepo.oss-cn-hongkong.aliyuncs.com/images/nextindex.jpg" alt="hexo" style="width:100%" /> 

## 前言  
Next主题是一款简洁大方、灵活、可定制的hexo主题，本文主要介绍了Next主题的基本配置、优化与风格定制。

<!-- more -->

## 添加、配置分类（标签、关于我）页面
当配置完Next主题后，还需要建立三个页面：分类页categories、标签页tags、关于页about，才能完善博客基本的内容，以创建分类页categories为例（其他两个页面步骤一样），创建页面的命令如下：

``` bash
hexo new page categories 
```

categories里index.md设置（comments：false，表示该页面禁用评论）：

```
---
title: 分类
date: 2018-01-29 23:12:48
type: "categories"
comments: false
---
```

创建、配置完三个页面之后，需要修改<span id="inline-purple">主题配置文件</span>中的对应配置：

```
menu:
  home: / || home
  about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
```

## 侧边栏头像设置
第一步，编辑<span id="inline-purple">主题配置文件</span>，修改字段avatar，值设置成头像的链接地址, 链接地址可以是完整的互联网URI或者站点内的地址。  
第二步，头像变成圆形，鼠标悬停有旋转效果，具体实现方法为，打开`\themes\next\source\css\_custom\custom.styl`，添加以下代码：

``` css
.site-author-image {
  display: block;
  margin: 0 auto;
  padding: $site-author-image-padding;
  max-width: $site-author-image-width;
  height: $site-author-image-height;
  border: $site-author-image-border-width solid $site-author-image-border-color;

  /* 头像圆形 */
  border-radius: 80px;
  -webkit-border-radius: 80px;
  -moz-border-radius: 80px;
  box-shadow: inset 0 -1px 0 #333sf;

  /* 设置循环动画 [animation: (play)动画名称 (2s)动画播放时长单位秒或微秒 (ase-out)动画播放的速度曲线为以低速结束 
    (1s)等待1秒然后开始动画 (1)动画播放次数(infinite为循环播放) ]*/
 

  /* 鼠标经过头像旋转360度 */
  -webkit-transition: -webkit-transform 1.0s ease-out;
  -moz-transition: -moz-transform 1.0s ease-out;
  transition: transform 1.0s ease-out;
}

img:hover {
  /* 鼠标经过停止头像旋转 
  -webkit-animation-play-state:paused;
  animation-play-state:paused;*/

  /* 鼠标经过头像旋转360度 */
  -webkit-transform: rotateZ(360deg);
  -moz-transform: rotateZ(360deg);
  transform: rotateZ(360deg);
}

/* Z 轴旋转动画 */
@-webkit-keyframes play {
  0% {
    -webkit-transform: rotateZ(0deg);
  }
  100% {
    -webkit-transform: rotateZ(-360deg);
  }
}
@-moz-keyframes play {
  0% {
    -moz-transform: rotateZ(0deg);
  }
  100% {
    -moz-transform: rotateZ(-360deg);
  }
}
@keyframes play {
  0% {
    transform: rotateZ(0deg);
  }
  100% {
    transform: rotateZ(-360deg);
  }
}
```

## 配置腾讯公益404页面
新建 404.html 页面，放到站点的 source 目录下，页面内容如下：

``` html
<!DOCTYPE HTML>
<html>
<head>
  <meta http-equiv="content-type" content="text/html;charset=utf-8;"/>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="robots" content="all" />
  <meta name="robots" content="index,follow"/>
  <link rel="stylesheet" type="text/css" href="https://qzone.qq.com/gy/404/style/404style.css">
</head>
<body>
  <script type="text/plain" src="http://www.qq.com/404/search_children.js"
          charset="utf-8" homePageUrl="/"
          homePageName="回到我的主页">
  </script>
  <script src="https://qzone.qq.com/gy/404/data.js" charset="utf-8"></script>
  <script src="https://qzone.qq.com/gy/404/page.js" charset="utf-8"></script>
</body>
</html>
```

## 添加本地搜索Local Search
第一步，安装 hexo-generator-searchdb，在站点的根目录下执行以下命令：

``` bash
npm install hexo-generator-searchdb --save
```

第二步，编辑<span id="inline-blue">站点配置文件</span>，新增以下内容到任意位置：

```
# Local Search
search:
  path: search.xml
  field: post
  format: html
  limit: 1000
```

第三步，编辑<span id="inline-purple">主题配置文件</span>，启用本地搜索功能：

```
# Local search
local_search:
  enable: true
```

## 配置文章阅读次数
访问[LeanClound](https://leancloud.cn "LeanClound")，注册账号并登陆，进行一番配置之后拿到AppID以及AppKey，然后编辑<span id="inline-purple">主题配置文件</span>，启用统计文章阅读次数功能：

```
leancloud_visitors:
  enable: true
  app_id: your appid
  app_key: your appkey
```

## 配置字数统计、阅读时长
第一步，安装hexo-symbols-count-time插件，在站点的根目录下执行以下命令：

``` bash
npm install hexo-symbols-count-time --save
```

第二步，编辑<span id="inline-blue">站点配置文件</span>，新增以下内容到任意位置：

```
# Page Count and Time
symbols_count_time:
  symbols: true
  time: true
```
第三步，编辑<span id="inline-purple">主题配置文件</span>，启用字数统计、阅读时长功能：

```
# Post wordcount display settings
# Dependencies: https://github.com/theme-next/hexo-symbols-count-time
symbols_count_time:
  separated_meta: true
  item_text_post: true
  item_text_total: false
  awl: 5
  wpm: 200
```

## 配置站点UV和PV统计
编辑<span id="inline-purple">主题配置文件</span>，配置busuanzi_count相关设置，如下所示：

```
# Show PV/UV of the website/page with busuanzi.
# Get more information on http://ibruce.info/2015/04/04/busuanzi/
busuanzi_count:
  # count values only if the other configs are false
  enable: true
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: <i class="fa fa-user"></i>
  site_uv_footer:
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: <i class="fa fa-eye"></i>
  site_pv_footer:
  # custom pv span for one page only
  page_pv: false
  page_pv_header: <i class="fa fa-file-o"></i>
  page_pv_footer:
```

## 配置来比力评论
Next主题支持多款评论系统，不过来比力的服务相对而言，比较稳定，首先访问[来比力](https://livere.com/ "来比力")，注册账号并登陆，获取uid字段，然后编辑<span id="inline-purple">主题配置文件</span>，启用来比力评论功能：

```
livere_uid: your uid
```

## 配置百度分享
编辑<span id="inline-purple">主题配置文件</span>，修改字段 baidushare，值为true，如下所示：

```
baidushare: 
  type: slide
  baidushare: true
```

## 配置RSS
第一步，安装hexo-generator-feed，在站点的根目录下执行以下命令：

``` bash
npm install --save hexo-generator-feed
```

第二步，编辑<span id="inline-blue">站点配置文件</span>，新增以下内容到任意位置：

```
# RSS
feed:
  type: atom
  path: atom.xml
  limit: 0
  hub:
  content: true
```

## 配置浏览进度
配置文章的浏览进度，编辑<span id="inline-purple">主题配置文件</span>，修改scrollpercent，值为true，如下所示：

```
# Scroll percent label in b2t button.
scrollpercent: true
```

## 配置打赏
配置打赏功能，编辑<span id="inline-purple">主题配置文件</span>，如下所示：

```
# Reward
reward_comment: 坚持原创技术分享，您的支持将鼓励我继续创作！
wechatpay: /images/wechatpay.jpg
alipay: /images/alipay.jpg
```

## 配置FancyBox
FancyBox插件，可以实现文章内的图片局部放大功能。  
第一步，下载theme-next-fancybox3，放在`\themes\next\source\lib`目录下。 
第二步，编辑<span id="inline-purple">主题配置文件</span>，修改fancybox，值为true，如下所示：

```
fancybox: true
```

## 添加Fork me On Github
先到[这里](https://blog.github.com/2008-12-19-github-ribbons/ "github-ribbons")，挑选自己喜欢的样式，并复制代码添加到`\themes\next\source\layout\_layout.swig`文件中(放在`<div class="headband"></div>`的下面)，并把href改为你的github地址，如下所示：

``` html
<!--添加Fork me on github -->
<a href="https://github.com/harderqian">
		<img style="position: absolute; top: 0; left: 0; border: 0;" src="https://camo.githubusercontent.com/c6286ade715e9bea433b4705870de482a654f78a/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f6c6566745f77686974655f6666666666662e706e67" alt="Fork me on GitHub" data-canonical-src="https://s3.amazonaws.com/github/ribbons/forkme_left_white_ffffff.png">
</a>
```

## 博文压缩优化
生成的静态文件存在大量空白，在一定程度上影响了网页加载，可以使用hexo-neat插件，对博文进行压缩优化。  
第一步，安装hexo-neat，在站点的根目录下执行以下命令：

``` bash
npm install hexo-neat --save
```

第二步，编辑<span id="inline-blue">站点配置文件</span>，新增以下内容到任意位置：

```
# hexo-neat
neat_enable: true

neat_html:
  enable: true
  exclude:
  
neat_css:
  enable: true
  exclude:
    - '*.min.css'

neat_js:
  enable: true
  mangle: true
  output:
  compress:
  exclude:
    - '*.min.js'
```

## 顶部添加加载进度条
第一步，先到[这里](https://github.com/theme-next/theme-next-pace "pace")，下载theme-next-pace，并放在`\themes\next\source\lib`目录下。   
第二步，编辑<span id="inline-purple">主题配置文件</span>，修改pace配置信息，如下所示：

```
# Progress bar in the top during page loading.
# Dependencies: https://github.com/theme-next/theme-next-pace
pace: true
# Themes list:
#pace-theme-big-counter
#pace-theme-bounce
#pace-theme-barber-shop
#pace-theme-center-atom
#pace-theme-center-circle
#pace-theme-center-radar
#pace-theme-center-simple
#pace-theme-corner-indicator
#pace-theme-fill-left
#pace-theme-flash
#pace-theme-loading-bar
#pace-theme-mac-osx
#pace-theme-minimal
# For example
# pace_theme: pace-theme-center-simple
pace_theme: pace-theme-flash
```

## 文章增加版权信息
在`\themes\next\layout\_macro\post.swig`模板中，加入版权信息div，如下所示：

```
{% else %}
{{ post.content }}

{### 版权信息---手动添加 ###}
<div align="center">
	<div class="copyright">
		<p>
		  <span>
			<b>本文地址：</b><a href="{{ url_for(page.path) }}" title="{{ page.title }}" style="color: #555;text-decoration: none;outline: none;border-bottom: 1px solid #ccc;word-wrap: break-word;">{{ page.permalink }}</a><br>
			<b>转载请注明出处，谢谢！</b>
		  </span>
		</p>
	</div>
</div>
{% endif  %}
</div>
{#####################}
{### END POST BODY ###}
{#####################}
```

## 更改文章底部的上一篇、下一篇顺序
在文章底部，有上下篇的链接（< >），但是点 > 发现进入的是页面中的的上面那篇文章，与操作习惯不符，别扭，这里修改一下顺序，修改`\theme\next\layout\_macro\post.swig`模板，具体修改如下所示：

```
{% if not is_index and (post.prev or post.next) %}
  <div class="post-nav">
    <div class="post-nav-next post-nav-item">
-      {% if post.next %}
+      {% if post.prev %}
-        <a href="{{ url_for(post.next.path) }}" rel="next" title="{{ post.next.title }}">
+        <a href="{{ url_for(post.prev.path) }}" rel="prev" title="{{ post.prev.title }}">
-          <i class="fa fa-chevron-left"></i> {{ post.next.title }}
+          <i class="fa fa-chevron-left"></i> {{ post.prev.title }}
        </a>
      {% endif %}
    </div>
    <span class="post-nav-divider"></span>
    <div class="post-nav-prev post-nav-item">
-      {% if post.prev %}
+      {% if post.next %}
-        <a href="{{ url_for(post.prev.path) }}" rel="prev" title="{{ post.prev.title }}">
+        <a href="{{ url_for(post.next.path) }}" rel="next" title="{{ post.next.title }}">
-          {{ post.prev.title }} <i class="fa fa-chevron-right"></i>
+          {{ post.next.title }} <i class="fa fa-chevron-right"></i>
        </a>
      {% endif %}
    </div>
  </div>
{% endif %}
```

## 主页文章添加阴影效果
给文章首页添加阴影效果，具体实现方法为，在`\themes\next\source\css\_custom\custom.styl`文件中，添加以下代码：

``` css
/*******首页文章阴影样式*******/
.post {
    margin-top: 60px;
    margin-bottom: 60px;
    padding: 25px;
    -webkit-box-shadow: 0 0 14px rgba(100, 100, 100, 0.5);
    -moz-box-shadow: 0 0 14px rgba(100, 100, 100, 0.5);
}
```

## 添加Readme.md文件
Hexo会把文件夹内的所有md文件，编译、解析成html，实现添加Readme.md文件，而且不会编译解析的具体方法为，编辑<span id="inline-blue">站点配置文件</span>，修改skip_render配置，如下所示：

```
skip_render: README.md
```

## 修改文章底部带#号的标签
具体实现方法为，修改模板`\themes\next\layout\_macro\post.swig`，搜索 `rel="tag">#`，将 `#` 换成`<i class="fa fa-tag"></i>`。

## 更改标签云颜色
默认的标签云页面，颜色搭配、字体大小可能看起来不太协调，修改标签云颜色的方法为，修改`\themes\next\layout\page.swig`模板，具体修改位置如下：

```
{{ tagcloud({min_font: 13, max_font: 31, amount: 1000, color: true, start_color: '#bbb', end_color: '#111'}) }}
```

>**提示：** tagcloud中的对应参数说明，见[Hexo官方TagCloud说明](https://hexo.io/zh-cn/docs/helpers.html#tagcloud "tagcloud")

## 代码块添加全选按钮
Hexo生成的博客中，代码片段是不支持选择全部功能的，若代码片段较长，手动选择非常的不方便，所以可以在代码块右侧添加一个全选按钮。具体实现方法为，在`\themes\next\layout\_layout.swig`模板中的`<head>`节点下添加如下代码：

``` javascript
<script src="//cdn.jsdelivr.net/jquery/2.1.3/jquery.min.js" language="JavaScript"></script>  
<script>  
	$(document).ready(function () {
	var SelectText = function(element) {
		var doc = document
			, text = element
			, range, selection
		;    
		if (doc.body.createTextRange) {
			range = document.body.createTextRange();
			range.moveToElementText(text);
			range.select();
		} else if (window.getSelection) {
			selection = window.getSelection();        
			range = document.createRange();
			range.selectNodeContents(text);
			selection.removeAllRanges();
			selection.addRange(range);
		}
	};

	$(".code").each(function() {
		var code = $(this).get(0);
		var button_html = 
			'<div style="position: fixed;'                                                               +
						'right: 3%;'                                                                     +
						'margin-top: 5px;'                                                               +
						'font-family: consolas, Menlo, \'PingFang SC\', \'Microsoft YaHei\', monospace;' +
						'font-size: 10px;'                                                               +
						'cursor: pointer;'                                                               +
						'color: #ff7600;'                                                                +
						'">'                                                                             +
			'<span>全选</span>'                                                                          +
			'</div>';
		var button = $(button_html);

		$(button).click(function() {
			SelectText(code);
		});
		$(button).insertBefore(this);
	});
}); 
</script> 
```

## 我的站点配置和主题配置
分享一下我的站点配置、主题配置以及主题的自定义样式，如有疏漏或者问题，欢迎大家在下面评论区交流。
我的站点配置如下：

```
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: HarderQian's Blog
subtitle: 生活、技术个人博客
description: Stay foolish，stay hungry！
author: HarderQian
language: zh-CN
timezone:

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://www.harderqian.cn
root: /
permalink: :title/
permalink_defaults:

# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render: README.md

# Writing
new_post_name: :title.md # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
future: true
highlight:
  enable: true
  line_number: true
  auto_detect: false
  tab_replace:
  
# Home page setting
# path: Root path for your blogs index page. (default = '')
# per_page: Posts displayed per page. (0 = disable pagination)
# order_by: Posts order. (Order by date descending by default)
index_generator:
  path: ''
  per_page: 10
  order_by: -date
  
# Category & Tag
default_category: uncategorized
category_map:
tag_map:

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  #repository: https://github.com/HarderQian/Harderqian.github.io.git
  repository: git@github.com:HarderQian/Harderqian.github.io.git
  branch: master
  
# Local Search
search:
  path: search.xml
  field: post
  format: html
  limit: 1000
 
# Page Count and Time
symbols_count_time:
  symbols: true
  time: true

# RSS
feed:
  type: atom
  path: atom.xml
  limit: 0
  hub:
  content: true

# Server
server:
  port: 4001
  compress: true
  header: true  
```

我的主题配置如下：

```
# ---------------------------------------------------------------
# Theme Core Configuration Settings
# ---------------------------------------------------------------

# If false, merge configs from `_data/next.yml` into default configuration (rewrite).
# If true, will fully override default configuration by options from `_data/next.yml` (override). Only for NexT settings.
# And if true, all config from default NexT `_config.yml` must be copied into `next.yml`. Use if you know what you are doing.
# Useful if you want to comment some options from NexT `_config.yml` by `next.yml` without editing default config.
override: false

# Allow to cache content generation. Introduced in NexT v6.0.0.
cache:
  enable: true

# Redefine custom file paths. Introduced in NexT v6.0.2.
# If commented, will be used default custom file paths.

# For example, you want to put your custom styles file
# outside theme directory in root `source/_data`, set
# `styles: source/_data/styles.styl`
#custom_file_path:
  # Default paths: layout/_custom/*
  #head: source/_data/head.swig
  #header: source/_data/header.swig
  #sidebar: source/_data/sidebar.swig

  # Default path: source/css/_variables/custom.styl
  #variables: source/_data/variables.styl
  # Default path: source/css/_mixins/custom.styl
  #mixins: source/_data/mixins.styl
  # Default path: source/css/_custom/custom.styl
  #styles: source/_data/styles.styl


# ---------------------------------------------------------------
# Site Information Settings
# ---------------------------------------------------------------

# To get or check favicons visit: https://realfavicongenerator.net
# Put your favicons into `hexo-site/source/` (recommend) or `hexo-site/themes/next/source/images/` directory.

# Default NexT favicons placed in `hexo-site/themes/next/source/images/` directory.
# And if you want to place your icons in `hexo-site/source/` root directory, you must remove `/images` prefix from pathes.

# For example, you put your favicons into `hexo-site/source/images` directory.
# Then need to rename & redefine they on any other names, otherwise icons from Next will rewrite your custom icons in Hexo.
favicon:
  small: /images/favicon-16x16-next.png
  medium: /images/favicon-32x32-next.png
  apple_touch_icon: /images/apple-touch-icon-next.png
  safari_pinned_tab: /images/logo.svg
  #android_manifest: /images/manifest.json
  #ms_browserconfig: /images/browserconfig.xml

# Set default keywords (Use a comma to separate)
keywords: Harderqian,Hexo,Next,博客

# Set rss to false to disable feed link.
# Leave rss as empty to use site's feed link.
# Set rss to specific value if you have burned your feed already.
rss:

footer:
  # Specify the date when the site was setup.
  # If not defined, current year will be used.
  #since: 2015

  # Icon between year and copyright info.
  icon: user

  # If not defined, will be used `author` from Hexo main config.
  copyright:
  # -------------------------------------------------------------
  # Hexo link (Powered by Hexo).
  powered: false

  theme:
    # Theme & scheme info link (Theme - NexT.scheme).
    enable: false
    # Version info of NexT after scheme info (vX.X.X).
    version: true
  # -------------------------------------------------------------
  # Any custom text can be defined here.
  #custom_text: Hosted by <a target="_blank" rel="external nofollow" href="https://pages.coding.me"><b>Coding Pages</b></a>

# ---------------------------------------------------------------
# SEO Settings
# ---------------------------------------------------------------

# Canonical, set a canonical link tag in your hexo, you could use it for your SEO of blog.
# See: https://support.google.com/webmasters/answer/139066
# Tips: Before you open this tag, remember set up your URL in hexo _config.yml ( ex. url: http://yourdomain.com )
canonical: true

# Change headers hierarchy on site-subtitle (will be main site description) and on all post/pages titles for better SEO-optimization.
seo: false

# If true, will add site-subtitle to index page, added in main hexo config.
# subtitle: Subtitle
index_with_subtitle: false


# ---------------------------------------------------------------
# Menu Settings
# ---------------------------------------------------------------

# When running the site in a subdirectory (e.g. domain.tld/blog), remove the leading slash from link value (/archives -> archives).
# Usage: `Key: /link/ || icon`
# Key is the name of menu item. If translate for this menu will find in languages - this translate will be loaded; if not - Key name will be used. Key is case-senstive.
# Value before `||` delimeter is the target link.
# Value after `||` delimeter is the name of FontAwesome icon. If icon (with or without delimeter) is not specified, question icon will be loaded.
menu:
  home: / || home
  about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #commonweal: /404/ || heartbeat

# Enable/Disable menu icons / item badges.
menu_settings:
  icons: true
  badges: false

# ---------------------------------------------------------------
# Scheme Settings
# ---------------------------------------------------------------

# Schemes
#scheme: Muse
scheme: Mist
#scheme: Pisces
#scheme: Gemini


# ---------------------------------------------------------------
# Sidebar Settings
# ---------------------------------------------------------------

# Posts / Categories / Tags in sidebar.
site_state: true

# Social Links.
# Usage: `Key: permalink || icon`
# Key is the link label showing to end users.
# Value before `||` delimeter is the target permalink.
# Value after `||` delimeter is the name of FontAwesome icon. If icon (with or without delimeter) is not specified, globe icon will be loaded.
social:
  GitHub: https://github.com/harderqian || github
  知乎: https://www.zhihu.com/people/qian-hong-liang-78
  Weibo: https://weibo.com/harderqian || weibo
  QQ: http://wpa.qq.com/msgrd?v=3&uin=781978505&site=qq&menu=yes || qq
  #Google: https://plus.google.com/yourname || google
  #Twitter: https://twitter.com/yourname || twitter
  #FB Page: https://www.facebook.com/yourname || facebook
  #VK Group: https://vk.com/yourname || vk
  #StackOverflow: https://stackoverflow.com/yourname || stack-overflow
  #YouTube: https://youtube.com/yourname || youtube
  #Instagram: https://instagram.com/yourname || instagram
  #Skype: skype:yourname?call|chat || skype

social_icons:
  enable: true
  icons_only: false
  transition: false

# Follow me on GitHub banner in right-top corner.
# Usage: `permalink || title`
# Value before `||` delimeter is the target permalink.
# Value after `||` delimeter is the title and aria-label name.
#github_banner: https://github.com/yourname || Follow me on GitHub

# Blog rolls
links_icon: link
links_title: Links
links_layout: block
#links_layout: inline
links:
  博客园: http://www.cnblogs.com/harderqian/

# Sidebar Avatar
# in theme directory(source/images): /images/avatar.gif
# in site  directory(source/uploads): /uploads/avatar.gif
avatar: /images/avatar.jpg

# Table Of Contents in the Sidebar
toc:
  enable: true

  # Automatically add list number to toc.
  number: true

  # If true, all words will placed on next lines if header width longer then sidebar width.
  wrap: false

# Creative Commons 4.0 International License.
# http://creativecommons.org/
# Available: by | by-nc | by-nc-nd | by-nc-sa | by-nd | by-sa | zero
#creative_commons: by-nc-sa
#creative_commons:

sidebar:
  # Sidebar Position, available value: left | right (only for Pisces | Gemini).
  position: left
  #position: right

  # Sidebar Display, available value (only for Muse | Mist):
  #  - post    expand on posts automatically. Default.
  #  - always  expand for all pages automatically
  #  - hide    expand only when click on the sidebar toggle icon.
  #  - remove  Totally remove sidebar including sidebar toggle.
  display: post
  #display: always
  #display: hide
  #display: remove

  # Sidebar offset from top menubar in pixels (only for Pisces | Gemini).
  offset: 12

  # Back to top in sidebar (only for Pisces | Gemini).
  b2t: false

  # Scroll percent label in b2t button.
  scrollpercent: true

  # Enable sidebar on narrow view (only for Muse | Mist).
  onmobile: false


# ---------------------------------------------------------------
# Post Settings
# ---------------------------------------------------------------

# Automatically scroll page to section which is under <!-- more --> mark.
scroll_to_more: true

# Automatically saving scroll position on each post/page in cookies.
save_scroll: false

# Automatically excerpt description in homepage as preamble text.
excerpt_description: true

# Automatically Excerpt. Not recommend.
# Please use <!-- more --> in the post to control excerpt accurately.
auto_excerpt:
  enable: false
  length: 150

# Post meta display settings
post_meta:
  item_text: true
  created_at: true
  updated_at: false
  # Only show 'updated' if different from 'created'.
  updated_diff: false
  categories: true

# Post wordcount display settings
# Dependencies: https://github.com/theme-next/hexo-symbols-count-time
symbols_count_time:
  separated_meta: true
  item_text_post: true
  item_text_total: false
  awl: 5
  wpm: 200

# Wechat Subscriber
#wechat_subscriber:
  #enabled: true
  #qcode: /path/to/your/wechatqcode ex. /uploads/wechat-qcode.jpg
  #description: ex. subscribe to my blog by scanning my public wechat account

# Reward
reward_comment: 坚持原创技术分享，您的支持将鼓励我继续创作！
wechatpay: /images/wechatpay.jpg
alipay: /images/alipay.jpg
#bitcoin: /images/bitcoin.png

# Declare license on posts
post_copyright:
  enable: false
  license: <a href="https://creativecommons.org/licenses/by-nc-sa/3.0/" rel="external nofollow" target="_blank">CC BY-NC-SA 3.0</a>


# ---------------------------------------------------------------
# Misc Theme Settings
# ---------------------------------------------------------------

# Reduce padding / margin indents on devices with narrow width.
mobile_layout_economy: false

# Android Chrome header panel color ($brand-bg / $headband-bg => $black-deep).
android_chrome_color: "#222"

# Custom Logo.
# !!Only available for Default Scheme currently.
# Options:
#   enabled: [true/false] - Replace with specific image
#   image: url-of-image   - Images's url
custom_logo:
  enabled: false
  image:

# Code Highlight theme
# Available value:
#    normal | night | night eighties | night blue | night bright
# https://github.com/chriskempson/tomorrow-theme
highlight_theme: night

# Enable "cheers" for archive page.
cheers_enabled: true

# ---------------------------------------------------------------
# Font Settings
# - Find fonts on Google Fonts (https://www.google.com/fonts)
# - All fonts set here will have the following styles:
#     light, light italic, normal, normal italic, bold, bold italic
# - Be aware that setting too much fonts will cause site running slowly
# - Introduce in 5.0.1
# ---------------------------------------------------------------
# CAUTION! Safari Version 10.1.2 bug: https://github.com/iissnan/hexo-theme-next/issues/1844
# To avoid space between header and sidebar in Pisces / Gemini themes recommended to use Web Safe fonts for `global` (and `logo`):
# Arial | Tahoma | Helvetica | Times New Roman | Courier New | Verdana | Georgia | Palatino | Garamond | Comic Sans MS | Trebuchet MS
# ---------------------------------------------------------------
font:
  enable: false

  # Uri of fonts host. E.g. //fonts.googleapis.com (Default).
  host:

  # Font options:
  # `external: true` will load this font family from `host` above.
  # `family: Times New Roman`. Without any quotes.
  # `size: xx`. Use `px` as unit.

  # Global font settings used on <body> element.
  global:
    external: true
    family: Lato
    size:

  # Font settings for Headlines (h1, h2, h3, h4, h5, h6).
  # Fallback to `global` font settings.
  headings:
    external: true
    family:
    size:

  # Font settings for posts.
  # Fallback to `global` font settings.
  posts:
    external: true
    family:

  # Font settings for Logo.
  # Fallback to `global` font settings.
  logo:
    external: true
    family:
    size:

  # Font settings for <code> and code blocks.
  codes:
    external: true
    family:
    size:


# ---------------------------------------------------------------
# Third Party Services Settings
# ---------------------------------------------------------------

# Math Equations Render Support
math:
  enable: false

  # Default(true) will load mathjax/katex script on demand
  # That is it only render those page who has 'mathjax: true' in Front Matter.
  # If you set it to false, it will load mathjax/katex srcipt EVERY PAGE.
  per_page: true

  engine: mathjax
  #engine: katex

  # hexo-rendering-pandoc (or hexo-renderer-kramed) needed to full MathJax support.
  mathjax:
    # For newMathJax CDN (cdnjs.cloudflare.com) with fallback to oldMathJax (cdn.mathjax.org).
    cdn: //cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML
    # For direct link to MathJax.js with CloudFlare CDN (cdnjs.cloudflare.com).
    #cdn: //cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_CHTML
    # For automatic detect latest version link to MathJax.js and get from CloudFlare.
    #cdn: //cdn.bootcss.com/mathjax/2.7.1/latest.js?config=TeX-AMS-MML_HTMLorMML

  # hexo-renderer-markdown-it-plus (or hexo-renderer-markdown-it with markdown-it-katex plugin)
  # needed to full Katex support.
  katex:
    # Use Katex 0.7.1 as default
    cdn: //cdnjs.cloudflare.com/ajax/libs/KaTeX/0.7.1/katex.min.css
    # If you want to try the latest version of Katex, use one below instead
    #cdn: //cdn.jsdelivr.net/katex/latest/katex.min.css

# Han Support
# Dependencies: https://github.com/theme-next/theme-next-han
han: false

# Pangu Support
# Dependencies: https://github.com/theme-next/theme-next-pangu
# For more information: https://github.com/vinta/pangu.js
pangu: false

# Swiftype Search API Key
#swiftype_key:

# Baidu Analytics ID
#baidu_analytics:

# Disqus
disqus:
  enable: false
  shortname:
  count: true
  lazyload: false

# Hypercomments
#hypercomments_id:

# changyan
changyan:
  enable: false
  appid: cyts1oSc1
  appkey: bfc3a2527df8cd12b47143667108d985


# Valine.
# You can get your appid and appkey from https://leancloud.cn
# more info please open https://valine.js.org
valine:
  enable: false
  appid: mjHGvqA1KFPbhXeRkfdA5BmM-gzGzoHsz
  appkey: eAc4JOdbXo6sWVPY7bv9TQIQ
  notify: false # mail notifier , https://github.com/xCss/Valine/wiki
  verify: false # Verification code
  placeholder: Just go go # comment box placeholder
  avatar: mm # gravatar style
  guest_info: nick,mail,link # custom comment header
  pageSize: 10 # pagination size


# Support for youyan comments system.
# You can get your uid from http://www.uyan.cc
#youyan_uid: 2156906

# Support for LiveRe comments system.
# You can get your uid from https://livere.com/insight/myCode (General web site)
livere_uid: MTAyMC8zMzg4NS8xMDQzOA==

# Gitment
# Introduction: https://imsun.net/posts/gitment-introduction/
gitment:
  enable: false
  mint: true # RECOMMEND, A mint on Gitment, to support count, language and proxy_gateway
  count: true # Show comments count in post meta area
  lazy: false # Comments lazy loading with a button
  cleanly: false # Hide 'Powered by ...' on footer, and more
  language: # Force language, or auto switch by theme
  github_user: # MUST HAVE, Your Github Username
  github_repo: # MUST HAVE, The name of the repo you use to store Gitment comments
  client_id: # MUST HAVE, Github client id for the Gitment
  client_secret: # EITHER this or proxy_gateway, Github access secret token for the Gitment
  proxy_gateway: # Address of api proxy, See: https://github.com/aimingoo/intersect
  redirect_protocol: # Protocol of redirect_uri with force_redirect_protocol when mint enabled

# Baidu Share
# Available value:
#    button | slide
# Warning: Baidu Share does not support https.
baidushare: 
  type: slide
  baidushare: true

# Share
# This plugin is more useful in China, make sure you known how to use it.
# And you can find the use guide at official webiste: http://www.jiathis.com/.
# Warning: JiaThis does not support https.
#jiathis:
  #uid: 2128442
  #jiathis: false
#add_this_id:


# NeedMoreShare2
# Dependencies: https://github.com/theme-next/theme-next-needmoreshare2
# See: https://github.com/revir/need-more-share2
# Also see: https://github.com/DzmVasileusky/needShareButton
# iconStyle: default | box
# boxForm: horizontal | vertical
# position: top / middle / bottom + Left / Center / Right
# networks: Weibo,Wechat,Douban,QQZone,Twitter,Linkedin,Mailto,Reddit,
#           Delicious,StumbleUpon,Pinterest,Facebook,GooglePlus,Slashdot,
#           Technorati,Posterous,Tumblr,GoogleBookmarks,Newsvine,
#           Evernote,Friendfeed,Vkontakte,Odnoklassniki,Mailru
needmoreshare2:
  enable: false
  postbottom:
    enable: false
    options:
      iconStyle: box
      boxForm: horizontal
      position: bottomCenter
      networks: Weibo,Wechat,Douban,QQZone,Twitter,Facebook
  float:
    enable: false
    options:
      iconStyle: box
      boxForm: horizontal
      position: middleRight
      networks: Weibo,Wechat,Douban,QQZone,Twitter,Facebook

# Google Webmaster tools verification setting
# See: https://www.google.com/webmasters/
#google_site_verification:

# Google Analytics
#google_analytics:

# Bing Webmaster tools verification setting
# See: https://www.bing.com/webmaster/
#bing_site_verification:

# Yandex Webmaster tools verification setting
# See: https://webmaster.yandex.ru/
#yandex_site_verification:

# CNZZ count
#cnzz_siteid:

# Application Insights
# See https://azure.microsoft.com/en-us/services/application-insights/
# application_insights:

# Post widgets & FB/VK comments settings.
# ---------------------------------------------------------------
# Facebook SDK Support.
# https://github.com/iissnan/hexo-theme-next/pull/410
facebook_sdk:
  enable:       false
  app_id:       #<app_id>
  fb_admin:     #<user_id>
  like_button:  #true
  webmaster:    #true

# Facebook comments plugin
# This plugin depends on Facebook SDK.
# If facebook_sdk.enable is false, Facebook comments plugin is unavailable.
facebook_comments_plugin:
  enable:       false
  num_of_posts: 10    # min posts num is 1
  width:        100%  # default width is 550px
  scheme:       light # default scheme is light (light or dark)

# VKontakte API Support.
# To get your AppID visit https://vk.com/editapp?act=create
vkontakte_api:
  enable:       false
  app_id:       #<app_id>
  like:         true
  comments:     true
  num_of_posts: 10

# Star rating support to each article.
# To get your ID visit https://widgetpack.com
rating:
  enable: false
  id:     #<app_id>
  color:  fc6423
# ---------------------------------------------------------------

# Show number of visitors to each article.
# You can visit https://leancloud.cn get AppID and AppKey.
leancloud_visitors:
  enable: true
  app_id: h2UO8HIhytuy9riUXzPrPIPm-gzGzoHsz
  app_key: tqbfRlld9BloI4uFs2PzGo6K

# Another tool to show number of visitors to each article.
# visit https://console.firebase.google.com/u/0/ to get apiKey and projectId
# visit https://firebase.google.com/docs/firestore/ to get more information about firestore
firestore:
  enable: false
  collection: articles #required, a string collection name to access firestore database
  apiKey: #required
  projectId: #required
  bluebird: false #enable this if you want to include bluebird 3.5.1(core version) Promise polyfill

# Show PV/UV of the website/page with busuanzi.
# Get more information on http://ibruce.info/2015/04/04/busuanzi/
busuanzi_count:
  # count values only if the other configs are false
  enable: true
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: <i class="fa fa-user"></i>
  site_uv_footer:
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: <i class="fa fa-eye"></i>
  site_pv_footer:
  # custom pv span for one page only
  page_pv: false
  page_pv_header: <i class="fa fa-file-o"></i>
  page_pv_footer:


# Tencent analytics ID
# tencent_analytics:

# Tencent MTA ID
# tencent_mta:


# Enable baidu push so that the blog will push the url to baidu automatically which is very helpful for SEO
baidu_push: false

# Google Calendar
# Share your recent schedule to others via calendar page
#
# API Documentation:
# https://developers.google.com/google-apps/calendar/v3/reference/events/list
calendar:
  enable: false
  calendar_id: <required>
  api_key: <required>
  orderBy: startTime
  offsetMax: 24
  offsetMin: 4
  timeZone:
  showDeleted: false
  singleEvents: true
  maxResults: 250

# Algolia Search
# Dependencies: https://github.com/theme-next/theme-next-algolia-instant-search
algolia_search:
  enable: false
  hits:
    per_page: 10
  labels:
    input_placeholder: Search for Posts
    hits_empty: "We didn't find any results for the search: ${query}"
    hits_stats: "${hits} results found in ${time} ms"

# Local search
# Dependencies: https://github.com/theme-next/hexo-generator-searchdb
local_search:
  enable: true
  # if auto, trigger search by changing input
  # if manual, trigger search by pressing enter key or search button
  trigger: auto
  # show top n results per article, show all results by setting to -1
  top_n_per_article: 1
  # unescape html strings to the readable one
  unescape: false

# Bookmark Support
# Dependencies: https://github.com/theme-next/theme-next-bookmark
bookmark:
  enable: false
  # if auto
  #   - save the reading position when closing the page
  #   - or clicking the bookmark-icon
  # if manual, only save it by clicking the bookmark-icon
  save: auto


# ---------------------------------------------------------------
# Tags Settings
# ---------------------------------------------------------------

# External URL with BASE64 encrypt & decrypt.
# Usage: {% exturl text url "title" %}
# Alias: {% extlink text url "title" %}
exturl: false

# Note tag (bs-callout).
note:
  # Note tag style values:
  #  - simple    bs-callout old alert style. Default.
  #  - modern    bs-callout new (v2-v3) alert style.
  #  - flat      flat callout style with background, like on Mozilla or StackOverflow.
  #  - disabled  disable all CSS styles import of note tag.
  style: simple
  icons: false
  border_radius: 3
  # Offset lighter of background in % for modern and flat styles (modern: -12 | 12; flat: -18 | 6).
  # Offset also applied to label tag variables. This option can work with disabled note tag.
  light_bg_offset: 0

# Label tag.
label: true

# Tabs tag.
tabs:
  enable: true
  transition:
    tabs: false
    labels: true
  border_radius: 0

# Reading progress bar
# Dependencies: https://github.com/theme-next/theme-next-reading-progress
reading_progress:
  enable: false
  color: "#37c6c0"
  height: 2px


#! ---------------------------------------------------------------
#! DO NOT EDIT THE FOLLOWING SETTINGS
#! UNLESS YOU KNOW WHAT YOU ARE DOING
#! ---------------------------------------------------------------

# Use velocity to animate everything.
motion:
  enable: true
  async: false
  transition:
    # Transition variants:
    # fadeIn | fadeOut | flipXIn | flipXOut | flipYIn | flipYOut | flipBounceXIn | flipBounceXOut | flipBounceYIn | flipBounceYOut
    # swoopIn | swoopOut | whirlIn | whirlOut | shrinkIn | shrinkOut | expandIn | expandOut
    # bounceIn | bounceOut | bounceUpIn | bounceUpOut | bounceDownIn | bounceDownOut | bounceLeftIn | bounceLeftOut | bounceRightIn | bounceRightOut
    # slideUpIn | slideUpOut | slideDownIn | slideDownOut | slideLeftIn | slideLeftOut | slideRightIn | slideRightOut
    # slideUpBigIn | slideUpBigOut | slideDownBigIn | slideDownBigOut | slideLeftBigIn | slideLeftBigOut | slideRightBigIn | slideRightBigOut
    # perspectiveUpIn | perspectiveUpOut | perspectiveDownIn | perspectiveDownOut | perspectiveLeftIn | perspectiveLeftOut | perspectiveRightIn | perspectiveRightOut
    post_block: fadeIn
    post_header: slideDownIn
    post_body: slideDownIn
    coll_header: slideLeftIn
    # Only for Pisces | Gemini.
    sidebar: slideUpIn

# Fancybox. There is support for old version 2 and new version 3.
# Please, choose only any one variant, do not need to install both.
# For install 2.x: https://github.com/theme-next/theme-next-fancybox
# For install 3.x: https://github.com/theme-next/theme-next-fancybox3
fancybox: true

# Added switch option for separated repo in 6.0.0.
# Dependencies: https://github.com/theme-next/theme-next-fastclick
fastclick: false

# Added switch option for separated repo in 6.0.0.
# Dependencies: https://github.com/theme-next/theme-next-jquery-lazyload
lazyload: false

# Progress bar in the top during page loading.
# Dependencies: https://github.com/theme-next/theme-next-pace
pace: true
# Themes list:
#pace-theme-big-counter
#pace-theme-bounce
#pace-theme-barber-shop
#pace-theme-center-atom
#pace-theme-center-circle
#pace-theme-center-radar
#pace-theme-center-simple
#pace-theme-corner-indicator
#pace-theme-fill-left
#pace-theme-flash
#pace-theme-loading-bar
#pace-theme-mac-osx
#pace-theme-minimal
# For example
# pace_theme: pace-theme-center-simple
pace_theme: pace-theme-flash

# Canvas-nest
# Dependencies: https://github.com/theme-next/theme-next-canvas-nest
canvas_nest: false

# JavaScript 3D library.
# Dependencies: https://github.com/theme-next/theme-next-three
# three_waves
three_waves: false
# canvas_lines
canvas_lines: false
# canvas_sphere
canvas_sphere: false

# Only fit scheme Pisces
# Dependencies: https://github.com/theme-next/theme-next-canvas-ribbon
# Canvas-ribbon
# size: The width of the ribbon.
# alpha: The transparency of the ribbon.
# zIndex: The display level of the ribbon.
canvas_ribbon:
  enable: false
  size: 300
  alpha: 0.6
  zIndex: -1

# Script Vendors.
# Set a CDN address for the vendor you want to customize.
# For example
#    jquery: https://ajax.googleapis.com/ajax/libs/jquery/2.2.0/jquery.min.js
# Be aware that you should use the same version as internal ones to avoid potential problems.
# Please use the https protocol of CDN files when you enable https on your site.
vendors:
  # Internal path prefix. Please do not edit it.
  _internal: lib

  # Internal version: 2.1.3
  jquery:

  # Internal version: 2.1.5
  # See: http://fancyapps.com/fancybox/
  fancybox:
  fancybox_css:

  # Internal version: 1.0.6
  # See: https://github.com/ftlabs/fastclick
  fastclick:

  # Internal version: 1.9.7
  # See: https://github.com/tuupola/jquery_lazyload
  lazyload:

  # Internal version: 1.2.1
  # See: http://VelocityJS.org
  velocity:

  # Internal version: 1.2.1
  # See: http://VelocityJS.org
  velocity_ui:

  # Internal version: 0.7.9
  # See: https://faisalman.github.io/ua-parser-js/
  ua_parser:

  # Internal version: 4.6.2
  # See: http://fontawesome.io/
  fontawesome:

  # Internal version: 1
  # https://www.algolia.com
  algolia_instant_js:
  algolia_instant_css:

  # Internal version: 1.0.2
  # See: https://github.com/HubSpot/pace
  # Or use direct links below:
  # pace: //cdn.bootcss.com/pace/1.0.2/pace.min.js
  # pace_css: //cdn.bootcss.com/pace/1.0.2/themes/blue/pace-theme-flash.min.css
  pace:
  pace_css:

  # Internal version: 1.0.0
  # https://github.com/hustcc/canvas-nest.js
  canvas_nest:

  # three
  three:

  # three_waves
  # https://github.com/jjandxa/three_waves
  three_waves:

  # three_waves
  # https://github.com/jjandxa/canvas_lines
  canvas_lines:

  # three_waves
  # https://github.com/jjandxa/canvas_sphere
  canvas_sphere:

  # Internal version: 1.0.0
  # https://github.com/zproo/canvas-ribbon
  canvas_ribbon:

  # Internal version: 3.3.0
  # https://github.com/ethantw/Han
  han:

  # Internal version: 3.3.0
  # https://github.com/vinta/pangu.js
  pangu:

  # needMoreShare2
  # https://github.com/revir/need-more-share2
  needMoreShare2:


# Assets
css: css
js: js
images: images

# Theme version
version: 6.0.3

```

我的主题自定义样式如下：

```
// Custom styles.

/**************************************************
                   首页样式
**************************************************/

/*******首页文章阴影样式*******/
.post {
    margin-top: 60px;
    margin-bottom: 60px;
    padding: 25px;
    -webkit-box-shadow: 0 0 14px rgba(100, 100, 100, 0.5);
    -moz-box-shadow: 0 0 14px rgba(100, 100, 100, 0.5);
}

/*******首页头部样式*******/
.header {
    background: url("/images/header-bk.jpg");
	height: 20vh;
}
.menu {
    float: none;
}
.logo-line-before,
.logo-line-after {
    display: none;
}
.menu .menu-item a {
    font-size: 14px;
    color: rgb(15, 46, 65);
    border-radius: 4px;
}
.site-meta {
	float: none;
    margin-left: 0px;
	margin-bottom: 15px;
    text-align: center;
}
.site-meta .site-title {
    font-size: 28px;
    font-family: 'Comic Sans MS', sans-serif;
    color: #fff;
}

/*******首页尾部样式*******/
.footer {
    background: none;
    font-size: 16px;
}
.footer-inner {
    font-family: 'Comic Sans MS', sans-serif;
    text-align: center;
    color: #4c618f;
}

/*******首页阅读全文样式*******/
.post-button {
    margin-top: 30px;
    text-align: center;
}
.post-button .btn {
    color: #fff;
    font-size: 15px;
    background: #686868;
    border-radius: 16px;
    line-height: 2;
    margin: 0 4px 8px 4px;
    padding: 0 20px;
}
.post-button a{
  border-bottom: 1px solid #666;
}
.post-button a:hover {
    color: #7784ba;
}


/**************************************************
                   侧边栏样式
**************************************************/

/******************侧边栏头像*******************/
.site-author-image {
  display: block;
  margin: 0 auto;
  padding: $site-author-image-padding;
  max-width: $site-author-image-width;
  height: $site-author-image-height;
  border: $site-author-image-border-width solid $site-author-image-border-color;

  /* 头像圆形 */
  border-radius: 80px;
  -webkit-border-radius: 80px;
  -moz-border-radius: 80px;
  box-shadow: inset 0 -1px 0 #333sf;

  /* 设置循环动画 [animation: (play)动画名称 (2s)动画播放时长单位秒或微秒 (ase-out)动画播放的速度曲线为以低速结束 
    (1s)等待1秒然后开始动画 (1)动画播放次数(infinite为循环播放) ]*/
 

  /* 鼠标经过头像旋转360度 */
  -webkit-transition: -webkit-transform 1.0s ease-out;
  -moz-transition: -moz-transform 1.0s ease-out;
  transition: transform 1.0s ease-out;
}

img:hover {
  /* 鼠标经过停止头像旋转 
  -webkit-animation-play-state:paused;
  animation-play-state:paused;*/

  /* 鼠标经过头像旋转360度 */
  -webkit-transform: rotateZ(360deg);
  -moz-transform: rotateZ(360deg);
  transform: rotateZ(360deg);
}

/* Z 轴旋转动画 */
@-webkit-keyframes play {
  0% {
    -webkit-transform: rotateZ(0deg);
  }
  100% {
    -webkit-transform: rotateZ(-360deg);
  }
}
@-moz-keyframes play {
  0% {
    -moz-transform: rotateZ(0deg);
  }
  100% {
    -moz-transform: rotateZ(-360deg);
  }
}
@keyframes play {
  0% {
    transform: rotateZ(0deg);
  }
  100% {
    transform: rotateZ(-360deg);
  }
}

/******************侧边栏信息样式*******************/
.site-author-name {
    color: #080808;
}
.links-of-blogroll {
    font-size: 14px;
    margin-bottom: 42px;
}
.links-of-author {
    margin-top: 30px;
    margin-bottom: 30px;
}
.sidebar {
	background: url(/images/bk.jpg);
	background-size: 320px 659px;
    background-position-y: 1vh;
    background-repeat: no-repeat;
    box-shadow: inset 2px 2px 40px #bdb2b2;
}
.sidebar-inner {
    color: #649ab6;
}
.sidebar a {
    color: #649ab6;
    border-bottom-color: #649ab6;
}
.sidebar a:hover {
    color: #0c0b0b;
	border-bottom-color: #0c0b0b;
}
.site-state-item {
    display: inline-block;
    padding: 8px 28px;
    border-left: 1px solid #649ab6;
}
.sidebar-nav .sidebar-nav-active {
    color: #649ab6;
    border-bottom-color: #649ab6;
}
.sidebar-nav .sidebar-nav-active:hover {
    color: #0c0b0b;
    border-bottom-color: #0c0b0b;
}
.sidebar-nav li:hover {
    color: #0c0b0b;
}
.feed-link {
    margin-top: 15px;
    margin-left: 7px;
}
.feed-link a {
    color: #649ab6;
    border: 1px solid #649ab6 !important;
    border-radius: 15px;
}
.feed-link a:hover {
    background-color: #649ab6;
}
.feed-link a i {
    color: #649ab6;
}

/******************侧栏按钮样式*******************/
.sidebar-toggle {
    background: #649ab6;
}
.page-post-detail .sidebar-toggle-line {
    background: #ffffff;
}
.back-to-top {
    background: #649ab6;
}

/******************文章目录样式*******************/
.post-toc .nav .active>a {
    color: #649ab6;
	border-bottom-color: #649ab6;
}
.post-toc .nav .active>a:hover {
    color: #649ab6;
	border-bottom-color: #649ab6;
}
.post-toc ol a:hover {
    color: #0c0b0b;
	border-bottom-color: #0c0b0b;
	font-weight: bold;
}

/**************************************************
                  LocalSearch框的样式
**************************************************/
.local-search-popup .search-icon, .local-search-popup .popup-btn-close{
	color: #649ab6;
}

/**************************************************
                 Post文章样式
**************************************************/

/******************文章超链接样式*******************/
.post-body p a {
    color: #649ab6;
	border-bottom-color: #649ab6;
}
.post-body p a:hover {
    color: #649ab6;
	border-bottom-color: #649ab6;
	font-weight: bold;
}

/******************文章块引用样式*******************/
blockquote {
    padding: 0 15px;
    color: #666;
    border-left: 4px solid #649ab6;
}

/******************文章内Span自定义样式*******************/
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

/******************行内代码样式*******************/
code {
    color: #ff7600;
    background: #fbf7f8;
    margin: 2px;
	border: 1px solid #c1c1c1;
}

/******************文章底部标签样式*******************/
.posts-expand .post-tags {
    text-align: center;
}
.posts-expand .post-tags a {
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    font-family: 'Comic Sans MS', sans-serif;
    transition: 0.2s ease-out;
}

```

## 总结
本文主要介绍了Next主题的配置与优化，主题的配置参考了网上很多相关博文的介绍，主题的优化与定制借鉴了很多优秀的个人博客（建议多用开发者工具，调试自己喜欢的元素style），文章有不足或者疏漏的地方，欢迎大家在下面评论区讨论。


