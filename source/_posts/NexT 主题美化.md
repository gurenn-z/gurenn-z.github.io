---
title: NexT 主题美化
date: 2019-06-14 22:40:21
tags: 
- Hexo
categories:
- Hexo
- NexT 主题小站美化
---

> 基于 **[NexT.Gemini v7.1.2](https://theme-next.org/)**，因为[官方文档](https://theme-next.iissnan.com/getting-started.html)有些设置不再适用，另外，网上的很多设置都是要改js代码，我发现最新版本的 NexT ，其实在**主题配置文件**中就可以轻易实现评论、头像旋转、修改文章底部标签图标、代码复制等更多功能，比网上动辄增删代码的方法简单多了……
>
> 这里记录下博客的每一次配置，做个备忘录o(╥﹏╥)o
>
> 持续更新，大概会又粗又长(｀・ω・´)~~

<!-- more -->

# 主题设定 #
编辑 **主题配置文件**，搜索 **scheme** ，有 Muse、Mist、Pisces、Gemini 四种可以选择，例如：
```yml
# Schemes
#scheme: Muse
#scheme: Mist
#scheme: Pisces
scheme: Gemini
```

# 设置语言 #
编辑 **站点配置文件**，将 language 设置成中文：
```yml
language: zh-CN
```

# 设置头像和站点描述 #
## 实现效果图 ##
![](https://i.loli.net/2019/06/17/5d0760052784c82502.gif)


## 具体实现 ##

编辑 **站点配置文件**：

```yml
# Site
title: # 网站标题
subtitle: # 副标题
description: #站点描述
keywords: # 网站关键字
author: # 作者昵称
language: zh-CN # 网站语言
timezone: # 时区
```

编辑 **主题配置文件**：
```yml
# Sidebar Avatar
avatar:
  # In theme directory (source/images): /images/avatar.gif 
  # 将头像放置在主题目录下的 source/images/ （若 images 目录不存在，则新建一个） 
  # 配置为：avatar: /images/avatar.png
  # In site directory (source/uploads): /uploads/avatar.gif
  # 将头像放置在站点目录下的 source/uploads/ （若 uploads 目录不存在，则新建一个）
  # 配置为：avatar: /uploads/avatar.png
  # You can also use other linking images.
  # 也可以放一个完整的互联网 url
  url: /images/avatar.jpg
  # If true, the avatar would be dispalyed in circle.
  # 设置头像为椭圆形
  rounded: true  
  # The value of opacity should be choose from 0 to 1 to set the opacity of the avatar.
  # 设置头像透明度，取值在[0, 1]
  opacity: 1  
  # If true, the avatar would be rotated with the cursor.
  # 设置头像是否旋转（这里默认是360°）
  rotated: true  
```
# 添加标签和分类页面 #
## 实现效果图 ##
![](https://i.loli.net/2019/06/17/5d0761a61ea1e80837.png)
![](https://i.loli.net/2019/06/17/5d0761a65575794278.png)

## 具体实现 ##
编辑 **主题配置文件**，添加 tags 和 categories：
```yml
menu:
  home: / || home
  #about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
```
在站点目录下，使用 hexo new page tags 新建一个标签页面：
```shell
$ hexo new page tags
```

在站点目录下，使用 hexo new page categories 新建一个分类页面：
```shell
$ hexo new page categories
```

执行成功后,在 source 目录下自动生成了的 tags 和 categories 文件，每个文件都含有一个 index.md
![](https://i.loli.net/2019/06/17/5d06fabe9e1e545137.png)

分别打开这两个 index.md，修改内容并保存：
`source/categories/index.md`:

```yml
---
title: categories
date: 2019-06-14 22:40:30
type: "分类"
---
```
`source/tags/index.md`:

```yml
---
title: tags
date: 2019-06-14 22:40:15
type: "标签"
---
```

这里就生成好了标签和分类的导航栏，要运用在文章中，就需就文章的开头添加 tags 和 categories 标签：
例如：

```yml
---
title: 小站基础设置
date: 2019-06-14 22:40:21
tags: 
- Hexo
categories:
- Hexo
- NexT 主题小站美化
---

```

<div class="note default"><p>

tips： 如果觉得每次都需要在文章头部手动添加 tags 和 categories 很麻烦，可以修改 `scaffolds/post.md`文件，例如：
```yml
---
title: {{ title }}
date: {{ date }}
tags:
categories:
---
```

这样，每次 `hexo new "article"` 后，生成的 md 文件会自动把 tags 和 categories 加到里面去。
</p></div>

# 修改文章底部的标签的图标 #
## 实现效果图 ##
![](https://i.loli.net/2019/06/17/5d07a780efb5624437.png)

## 具体实现 ##
编辑 **主题配置文件**，搜索 **tag_icon** 一项，将 false 改为 true，修改内容：
```yml
# Use icon instead of the symblo # to indicate the tag at the bottom of the post
tag_icon: true
```

# 隐藏小站底部的 Powered by Hexo 和 Theme - NexT.scheme #
## 原效果 ##
![](https://i.loli.net/2019/06/17/5d07abbfe959147246.png)
## 实现效果图 ##
![](https://i.loli.net/2019/06/17/5d07ac9eacfd020855.png)
## 具体实现 ##
编辑 **主题配置文件**，搜索 powered 和 theme ，将 true 都设为 false：
```yml
  powered:
    # Hexo link (Powered by Hexo).
    enable: false
    # Version info of Hexo after Hexo link (vX.X.X).
    version: false

  theme:
    # Theme & scheme info link (Theme - NexT.scheme).
    enable: false
    # Version info of NexT after scheme info (vX.X.X).
    version: false
```

# 代码复制 #
## 实现效果图 ##
![](https://i.loli.net/2019/06/17/5d07b236f2a1b97760.gif)
## 具体实现 ##
编辑 **主题配置文件**，搜索 codeblock，将 copy_button 中的 **enable** 和 **show_result** 这两项设为 true：
```yml
codeblock:
  # Manual define the border radius in codeblock, leave it blank for the default value: 1
  border_radius:
  # Add copy button on codeblock
  copy_button:
    enable: true
    # Show text copy result
    show_result: true
    # Style: only 'flat' is currently available, leave it blank if you prefer default theme
    style:
```

# 在文章段落中添加 Note Tag

## 实现效果图

<div class="note default"><p> 
    tips：小技巧

 在文章段落中添加 Note Tag
    
</p></div>

## 具体实现

编辑 **主题配置文件**，搜索 note，可以修改 `style`、`icons` 和 `border_radius`，例如：

```yml
note:
  # Note tag style values:
  #  - simple    bs-callout old alert style. Default.
  #  - modern    bs-callout new (v2-v3) alert style.
  #  - flat      flat callout style with background, like on Mozilla or StackOverflow.
  #  - disabled  disable all CSS styles import of note tag.
  style: simple
  icons: true
  border_radius: 3
  # Offset lighter of background in % for modern and flat styles (modern: -12 | 12; flat: -18 | 6).
  # Offset also applied to label tag variables. This option can work with disabled note tag.
  light_bg_offset: 0
```

在文章中需要添加的地方加上：

```html
<div class="note default"><p> 某段话 </p></div>
```

其中 `class` 中参数可以有多种选择，最终效果也不一样，例如：

```html
<div class="note default"><p> tips：  </p></div>
```

<div class="note default"><p> tips：  </p></div>

```html
<div class="note primary"><p> primary：  </p></div>
```

<div class="note primary"><p> primary：  </p></div>

```html
<div class="note success"><p> success：  </p></div>
```

<div class="note success"><p> success：  </p></div>

```html
<div class="note info"><p> info：  </p></div>
```

<div class="note info"><p> info：  </p></div>

```html
<div class="note warning"><p> warning：  </p></div>
```

<div class="note warning"><p> warning：  </p></div>

```html
<div class="note danger"><p> danger：  </p></div>
```

<div class="note danger"><p> danger：  </p></div>

```html
<div class="note danger no-icon"><p> danger no-icon：  </p></div>
```

<div class="note danger no-icon"><p> danger no-icon：  </p></div>

# 修改文章中的文本链接样式

## 实现效果图

![](https://i.loli.net/2019/06/18/5d08b63339c8a59020.gif)

## 具体实现

编辑文件 `themes/next/source/css/_common/components/post/post.styl`，添加如下内容：

```styl
// 文章内链接文本样式
.post-body p a{
  color: #0593d3;
  border-bottom: none;
  border-bottom: 1px solid #0593d3;
  &:hover {
    color: #fc6423;
    border-bottom: none;
    border-bottom: 1px solid #fc6423;
  }
}
```

# 保存源码到 GitHub

## 效果图

![](https://myblog-hexo-1256211006.cos.ap-chengdu.myqcloud.com/hexo/NexT主题美化/20190731185943.png)

## 具体实现

```bash
git init
git remote add origin https://github.com/gurenn-z/gurenn-z.github.io.git
git add .
git commit -m "源码备份"
git push origin master:source-next
```



# 字数统计和阅读时长

## 效果图

![](https://myblog-hexo-1256211006.cos.ap-chengdu.myqcloud.com/hexo/NexT主题美化/20190731203220.png)

![](https://myblog-hexo-1256211006.cos.ap-chengdu.myqcloud.com/hexo/NexT主题美化/20190731214438.png)

## 具体实现

安装统计功能插件 ：

```bash
npm install hexo-symbols-count-time --save
```

编辑 **站点配置文件** ，添加如下：

```yml
symbols_count_time:
  # 文章内是否显示
  symbols: true # 本文字数
  time: true # 阅读时长
  # 网页底部是否显示
  total_symbols: true # 站点总字数
  total_time: true # 站点阅读时长
```

编辑 **主题配置文件** ，找到 `symbols_count_time` 一项，修改如下：

```yml
symbols_count_time:
  separated_meta: true
  item_text_post: true
  item_text_total: true
  awl: 4
  wpm: 275
```

# 访客人数、访客量、阅读统计 —— 不蒜子

## 效果图

![](https://myblog-hexo-1256211006.cos.ap-chengdu.myqcloud.com/hexo/NexT主题美化/20190731215122.png)

![](https://myblog-hexo-1256211006.cos.ap-chengdu.myqcloud.com/hexo/NexT主题美化/20190731215502.png)

## 具体实现

编辑 **主题配置文件** ，找到 `busuanzi_count` 一项（主题 6 以上已集成了 busuanzi 插件），修改如下：

```yml
busuanzi_count:
  enable: true
  total_visitors: true
  total_visitors_icon: user
  total_views: true
  total_views_icon: eye
  post_views: true
  post_views_icon: eye
```

可以修改 `themes/next/layout_third-party/analytics` 下的 `busuanzi-counter.swig` 文件，添加底部统计说明，例如：

![](https://myblog-hexo-1256211006.cos.ap-chengdu.myqcloud.com/hexo/NexT主题美化/20190731215420.png)