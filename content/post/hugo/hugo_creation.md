---
title: "从零开始搭建个人博客（一）- 使用hugo搭建个人博客"
date: 2021-11-23T01:00:55+08:00
tags : [
"hugo",
]
categories : [
"hugo",
]
keywords : [
"hugo",
]
---

原文地址：[https://left-pocket.github.io](https://left-pocket.github.io/post/hugo/hugo_creation/)

# 背景
使用个人博客也有一年多的时间，这一年多的时候踩了很多坑，也学到了很多知识。  
这里分享一个系列教程：**从零开始搭建个人博客**，把我的经验分享在这里。  
系列地址：[https://left-pocket.github.io](https://left-pocket.github.io/post/hugo/hugo_0/)

# 从零开始搭建个人博客（一）- 使用hugo搭建个人博客

### 介绍
很多人都想搭建个人博客，不知道怎么做。实际上现在市场上有很多静态博客生成器。这个生成器会帮你生成一个静态博客的内容，而你只需要关注你的博客的每一篇内容就可以。  
比较常用的个人博客生成器有：
* Jekyll
* Hugo
* Hexo

我这里悬着Hugo来搭建我的个人博客，因为它简单，快速，开源，使用Go语言，社区活跃等优点。

### hugo
hugo 是由Go语言实现的静态网站生成器。简单，易用，高效，易扩展。

### 安装
我这边介绍在macOS上的安装教程。其他环境（Windows/linux）类似。

```
>>> brew install hugo
>>> hugo version
hugo v0.89.4+extended darwin/arm64 BuildDate=unknown
```

### 创建站点
创建一个站点 **left-pocket-test**， 并进入到站点根目录。
这个站点命名没那么重要，可以随意取名。
```
>>> hugo new site left-pocket-test
>>> cd left-pocket-test
>>> ls
archetypes  content     layouts     resources   themes
config.toml data        public      static
```

**config.toml** 是配置文件，在里面可以定义博客地址，构建配置，标题，导航栏等等。
**themes**是主题目录，可以下载喜欢的主题，然后配置在**config.toml**里面。
**content**是博客文章的目录。
**static**是博客的静态资源，比如图片
**public**是编译后的目标文件的目录。

注：当前目录是你的**源文件**，也就是包括一堆模版，博客源文件（markdown），配置文件，图片的一个源文件的集合。
最终展示在网页的是**目标文件**，也就根据你的资源和配置，最终生成的一个个包括css，js的html文件集合。

### 主题
在最终我们的博客可以运行之前，我们需要配置一个主题。

推荐一款主题，可以在根目录下载并配置。  
可以去官方主题网站：[https://themes.gohugo.io/](https://themes.gohugo.io/)  
挑选你喜欢的主题。

我们选择一款比较活跃的主题：[Even](https://github.com/olOwOlo/hugo-theme-even)

安装主题：
```
git clone https://github.com/olOwOlo/hugo-theme-even themes/even
```

这个时候even这个主题就被下载到**themes**目录下。

**注**：如果是从其他地方copy过来的站点，有可能遇到:
```
WARN 2021/02/03 10:56:17 found no layout file for "HTML" for kind "home": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
```
这个时候需要重新**git clone**一下主题。

### 配置
下载好主题后，主题的**exampleSite**目录一般会有一个**config.toml**配置文件。复制到你的根目录下的**config.tmol**文件，然后根据注释做一些基本的修改。

这是我复制下来的配置做的一些简单的修改：
```
baseURL = "http://localhost:1313/"
languageCode = "en"
defaultContentLanguage = "en"                             # en / zh-cn / ... (This field determines which i18n file to use)
title = "Leftpocket的个人博客"
preserveTaxonomyNames = true
enableRobotsTXT = true
enableEmoji = true
theme = "even"
enableGitInfo = false # use git commit log to generate lastmod record # 可根据 Git 中的提交生成最近更新记录。

# Syntax highlighting by Chroma. NOTE: Don't enable `highlightInClient` and `chroma` at the same time!
pygmentsOptions = "linenos=table"
pygmentsCodefences = true
pygmentsUseClasses = true
pygmentsCodefencesGuessSyntax = true

hasCJKLanguage = true     # has chinese/japanese/korean ? # 自动检测是否包含 中文\日文\韩文
paginate = 5                                              # 首页每页显示的文章数
disqusShortname = ""      # disqus_shortname
googleAnalytics = ""      # UA-XXXXXXXX-X
copyright = ""            # default: author.name ↓        # 默认为下面配置的author.name ↓

[author]                  # essential                     # 必需
  name = "Leftpocket"

[sitemap]                 # essential                     # 必需
  changefreq = "weekly"
  priority = 0.5
  filename = "sitemap.xml"

[[menu.main]]             # config your menu              # 配置目录
  name = "Home"
  weight = 10
  identifier = "home"
  url = "/"
[[menu.main]]
  name = "Archives"
  weight = 20
  identifier = "archives"
  url = "/post/"
[[menu.main]]
  name = "Tags"
  weight = 30
  identifier = "tags"
  url = "/tags/"
[[menu.main]]
  name = "Categories"
  weight = 40
  identifier = "categories"
  url = "/categories/"

[params]
  version = "4.x"           # Used to give a friendly message when you have an incompatible update
  debug = false             # If true, load `eruda.min.js`. See https://github.com/liriliri/eruda

  since = "2017"            # Site creation time          # 站点建立时间
  # use public git repo url to link lastmod git commit, enableGitInfo should be true.
  # 指定 git 仓库地址，可以生成指向最近更新的 git commit 的链接，需要将 enableGitInfo 设置成 true.
  gitRepo = ""

  # site info (optional)                                  # 站点信息（可选，不需要的可以直接注释掉）
  logoTitle = "Leftpocket的个人博客"        # default: the title value    # 默认值: 上面设置的title值
  keywords = ["Hugo", "theme","even"]
  description = "Hugo theme even example site."

  # paginate of archives, tags and categories             # 归档、标签、分类每页显示的文章数目，建议修改为一个较大的值
  archivePaginate = 50

  # show 'xx Posts In Total' in archive page ?            # 是否在归档页显示文章的总数
  showArchiveCount = false

  # The date format to use; for a list of valid formats, see https://gohugo.io/functions/format/
  dateFormatToUse = "2006-01-02"

  # show word count and read time ?                       # 是否显示字数统计与阅读时间
  moreMeta = false

  # Syntax highlighting by highlight.js
  highlightInClient = false

 # 后续省略，可直接从 **themes/exampleSite/config.toml** 下复制到跟目录下进行修改。
```

具体的高级配置，会在后续的高级配置详细介绍，我们这一篇主要讲解基础配置。
暂时只需要修改 **title** 和 **autohr** 相关的内容就可以了。
```
title = "Leftpocket的个人博客"
logoTitle = "Leftpocket的个人博客"

[author]                  # essential                     # 必需
  name = "Leftpocket"
```

### 发布第一篇文章
配置完成后，发布第一篇文章。
```
hugo new post/my-first-post.md
```
其中有着 draft 选项。当 draft 为 true 的时候，默认是不会渲染的，渲染 draft 需要加 **-D** 的启动参数。 我们可以将 draft 改为 false，这样默认就可以渲染了。  
一般来说，把**draft: true**去掉，加一些markdown语法的内容就可以了。  
后续可以直接自己直接在编辑器里面 **content/post/**目录下创建 **md** 文件来写博客。比较方便。也可以在post里面创建多层目录，方便归类。

这是我的文章配置。

```
---
title: "My First Post"
date: 2021-11-28T16:46:27+08:00
tags : [
"hugo",
]
categories : [
"hugo",
]
keywords : [
"hugo",
]
---
This is the first post.
```

### 执行命令

```
>>> hugo server

                   | EN  
-------------------+-----
  Pages            | 11  
  Paginator pages  |  0  
  Non-page files   |  0  
  Static files     |  5  
  Processed images |  0  
  Aliases          |  2  
  Sitemaps         |  1  
  Cleaned          |  0  

Built in 21 ms
Watching for changes in /Users/hugo/iwtbabc/{archetypes,content,data,layouts,static,themes}
Watching for config changes in /Users/hugo/iwtbabc/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

在浏览器输入 [http://localhost:1313/](http://localhost:1313/)  即可看到具体效果。  
其中文章中，可以设置 `tag`, `categories`, `keywords`等属性。

![Settings](/img/hugo/hugo_create.png)

Demo完成，我们现在可以在本地浏览器上浏览你的hugo博客。  
你也可以查看配置的描述，自己尝试修改配置的一些参数，看一下浏览器的效果。比如说你可以把页面里面的英文标签改为中文的，直接在配置里面修改就行。  
hugo是立即生效的，不需要重新启动。

如果需要插入图片，需要放在static目录下：
比如我们添加一张图片 `static/img/test.png`
那么在md文章里面插入：
```
![test图片](/img/test.png)
```
即可正常显示。

下一篇将具体讲如何把hugo博客托管到github Pages上。就相当于部署到了服务器上，这样你就可以随时随地查看你的博客了。

<全文完>

欢迎关注我的微信公众号：**码农在新加坡**，有更多好的技术分享。
![pic](/img/personal/qrcode_2.png)