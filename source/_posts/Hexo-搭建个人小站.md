---
title: Hexo 搭建个人小站
date: 2019-06-14 18:03:43
tags:
- Hexo
categories:
- Hexo
---

> 我搭建博客采用的方式是 **GitHub Pages** + **Hexo**
> 
> 中间因为万恶的强迫症，试了各种插件，结果越弄越糟，干脆删了重建，顺便记录我的每一次操作，呕血写出这篇记录。


<!-- more -->

# 创建 GitHub Pages #


1. 在GitHub上创建一个仓库，仓库名为 `<username>.github.io`。 其中，`<username>` 必须与 owner 相同，这样就可以直接通过 仓库名 来访问网页了。
![20190614161454.png](https://i.loli.net/2019/06/14/5d0357a8536b715656.png)

2. 创建后，在 **Settings** 页面下 找到 **GitHub Pages** 一项，

	![20190614161606.png](https://i.loli.net/2019/06/14/5d0357e1f0b4e58703.png)

	![20190614161754.png](https://i.loli.net/2019/06/14/5d03584a029d944311.png)


3. 现在已经可以访问我们的 GitHub Pages 了（如果 site 没有被published，在 Source 中选择 **master branch**）

	![20190614162233.png](https://i.loli.net/2019/06/14/5d035969f1c2951487.png)

# 安装 Hexo #

Hexo基于 [Git](https://git-scm.com/) 和 [NodeJs](http://nodejs.org/)，这两项是必须要先安装的。

网上有很详细的安装教程，比如：

[http://https://www.runoob.com/git/git-install-setup.html](http://www.runoob.com/git/git-install-setup.html "Git 安装")

[http://https://www.runoob.com/nodejs/nodejs-install-setup.html](http://www.runoob.com/nodejs/nodejs-install-setup.html "NodeJs 安装")

接下来只需要使用 npm 即可完成 Hexo 的安装。（Windows下打开cmd窗口执行即可，它会安装在你的NodeJs目录下。可能需要翻墙。）

```shell
    $ npm install -g hexo-cli
```

# 启动博客 #

- 新建一个自己的博客文件夹，比如 **MyBlog**
- 进入该文件夹，右键，Git Bash Here，依次执行下列命令，Hexo 就会在创建所需要的文件

	```bash
		$ hexo init <folder>
		$ cd <folder>
		$ npm install
	```

	比如，
	![20190614165824.png](https://i.loli.net/2019/06/14/5d0361d04bd4428594.png)

	![20190614165946.png](https://i.loli.net/2019/06/14/5d036217276c484540.png)
	
- 本地启动博客

	```shell
		$ hexo s  #（hexo server 的缩写，两者命令效果相同）启动本地 hexo
	```

	![20190614170217.png](https://i.loli.net/2019/06/14/5d0362b3ab66a29395.png)

- 本地访问及调试： `localhost:400`

	![20190614170741.png](https://i.loli.net/2019/06/14/5d0363f3346d635650.png)

# 博客目录 #

可以看到，博客文件夹下的目录结构是这样的：
```yml
		.
	├── _config.yml  # 站点配置文件，可以配置大部分的参数
	├── package.json # 应用程序的信息，可以自由删除
	├── scaffolds    # 模版文件夹。我们新建的文章都是根据 scaffold 来建立的，比如设置文章的标签、分类等。 
	├── source	 # 资源文件夹，存放用户资源
	|   ├── _drafts
	|   └── _posts   # 我们新建的博客文章就放在这里
	└── themes	 # 主题文件夹。 可以下载不同的主题（博客风格样式）放在这里，然后在站点配置文件中设置当前主题，Hexo会根据主题来生成静态页面。
```

# Hexo 与 GitHub 关联 #
首先，安装插件 [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)
```bash
$ npm install hexo-deployer-git --save
```
![20190614173717.png](https://i.loli.net/2019/06/14/5d036ae703aab17844.png)

（它会存放在 **node_modules** 文件夹下。）

然后，在**站点配置文件** `_config.yml` 中 找的 **deploy** 项，配置如下（ps：**配置文件中 键 和值 之间必须要有一个空格**）:

![20190614173201.png](https://i.loli.net/2019/06/14/5d0369b0a937d82019.png)

在 **git bash** 中执行命令 `$ hexo clean && hexo g && hexo d`，将本地文件部署到远程库中去

说明：
```bash
$ hexo clean     # 清除站点文件
$ hexo g	 # （hexo generate 的缩写，两者命令效果相同）生成本地静态文件
$ hexo d	 # （hexo deploy 的缩写，两者命令效果相同）重新生成站点文件并将之推送到指定的库分支
```

此时就可用的 GitHub Page 来访问我们的博客了。
![20190614175823.png](https://i.loli.net/2019/06/14/5d036fe7ead1b45819.png)

# 第一篇文章 #

进入博客根目录，在 **source** 目录下 的 **_post** 文件夹中执行命令 `hexo new <title>`，创建一篇新的博客。

![20190614180518.png](https://i.loli.net/2019/06/14/5d0371737fabd35253.png)

`hexo s` 在本地调试后，再 `hexo clean && hexo g && hexo d` 推送到 GitHub 上去



# 选择风格主题 #

这里挑了 NexT 主题

由于[这个地址](https://github.com/iissnan/hexo-theme-next)的仓库不再维护了，因此我下载了活跃社区的 [NexT](https://github.com/theme-next/hexo-theme-next)

进入博客根目录，在 **git bash** 中执行：
```shell
$ git clone https://github.com/theme-next/hexo-theme-next themes/next
```
下载的主题存放在 theme 目录中。


在**站点配置文件**中，找到 **theme** 项，设置主题：

![20190614200711.png](https://i.loli.net/2019/06/14/5d038e111e7e656509.png)

[关于 Hexo 的官方文档，戳这里](https://hexo.io/zh-cn/docs/index.html)

[关于 NexT 的官方文档，戳这里](https://theme-next.iissnan.com/)

