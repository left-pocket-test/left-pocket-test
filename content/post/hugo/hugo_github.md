---
title: "从零开始搭建个人博客（二）- 把hugo博客托管到github上"
date: 2021-11-23T01:00:59+08:00
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

原文地址：[https://left-pocket.github.io](https://left-pocket.github.io/post/hugo/hugo_github/)

# 背景
使用个人博客也有一年多的时间，这一年多的时候踩了很多坑，也学到了很多知识。  
这里分享一个系列教程：**从零开始搭建个人博客**，把我的经验分享在这里。  
系列地址：[https://left-pocket.github.io](https://left-pocket.github.io/post/hugo/hugo_0/)

# 从零开始搭建个人博客（二）- 把hugo博客托管到github上
上一篇文章，我们学习了怎么搭建个人博客，但是只是在局域网内运行，现在我们要把博客部署到互联网中。  
如果你没有自己的云服务器，不要慌，我们可以把个人博客搭建在`Github Pages`中，就跟搭建在自己的服务器一样。  
`Github Pages`是Github提供的一个静态网站托管服务，可以用于存放静态网页，包括博客，项目文档甚至整本书。非常适合我们搭建个人博客。

### 创建Github Pages
要想把个人博客托管在Github Pages上，首先你需要有一个Github账号，作为程序员，应该每个人都有自己的Github账号。  
下面我介绍下怎么部署在Github Pages上：  
假设你需要部署在 GitHub Pages 上，首先在GitHub上创建一个Repository，命名为：`{your_username}.github.io`. 比如我的Repo就叫 `left-pocket-test.github.io`。  
如果你对你的username不满意，需要先在`Setting->Account->Change username`修改一个你满意的username。  
**注：** Repository的前缀一定要跟你的username保持一致。

![Settings](/img/hugo/github_create.png)

Repo的权限需要选择Public, 否则无法访问。  
勾选`Add a README.md`，主要是为了自动创建main分支。

然后在你的Repo里面点击Settings, 下拉，找到Github Pages。

![Settings](/img/hugo/github_setting.png)
![Github Pages](/img/hugo/github_pages.png)

点击**Change Theme** 选择一款主题，保存。  
这里随便选择一款，因为后续托管Hugo博客之后现在的设置就覆盖了，选择后会提示：`Your site is published at https://left-pocket-test.github.io/`。 

![Github Pages](/img/hugo/github_page2.png)


过几分钟之后，通过访问
[https://left-pocket-test.github.io/](https://left-pocket-test.github.io/) 能正常打开，说明github Page设置正常。
![Github Pages](/img/hugo/github_page3.png)

### 初始化hugo博客
这个在上一篇文章里面有讲解：如果有疑问可以回顾上一篇文章。
[从零开始搭建个人博客（一）- 使用hugo搭建个人博客](https://left-pocket.github.io/post/hugo/hugo_creation/)

### 发布hugo到github
现在我们有了Hugo博客，有了Github Pages，那么下一步就是把hugo博客发布到github。这样我们才能在互联网的任何地方访问我们的博客。  
在我们本地的hugo根目录中执行 **hugo** 指令。会生成一个public文件夹，我们只需要把public的文件夹上传到github上刚才创建的Repo里面, 一分钟左右，就能正常查看博客内容。

**这里解释一下**
- hugo站点：这个是原始内容，可以不用提交到github，也可以选择在github上创建一个新的repo，并提交。
- hugo站点内的public目录(软链接)：这个是使用**hugo**指令生成的发布内容，需要发布到Github Pages上。

我们的hugo站点是**源文件** （带主题，图片，markdown源文件），public是**目标文件**（最终生成的css/js/html文件）。我们最终网页上展示的是目标文件，所以需要使用**hugo**指令生成目标文件。

### 使用git指令发布到github
这种方式更简单一点，推荐使用这一种方式：
在任意hugo站点外，直接用git clone把创建好的github pages Repo克隆下来。
```
git clone git@github.com:left-pocket-test/left-pocket-test.github.io.git
```
然后创建把这个`git Repo目录`和hugo站点的根目录的`public`创建软链接：
```
ln -s /Users/hugo/left-pocket-test.github.io /Users/hugo/left-pocket-test/public
```
然后在`hugo站点`使用**hugo**指令，就会自动在public软链接也就是git repo下生成目标文件。  
最终执行git add/commit/push之后，打开  
https://left-pocket-test.github.io/  
就能看到博客内容。 (可能有几分钟延迟，耐心等待)。

![Github Pages](/img/hugo/github_hugo.png)

如果git push提示没有权限：
```
ERROR: Permission to left-pocket-test/left-pocket-test.github.io.git denied to left-pocket.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
```
那就在Github上添加一下ssh key就好了。

现在我们`left-pocket-test.github.io`存放的是目标文件，有些人也想把hugo站点文件，也就是源文件也上传到github保存。  
那么在Github上另创一个Repo来保存源文件也是可以的，源文件对最终的展示效果没有影响，只是为了方便保存。我个人创建了一个单独的hugo仓库来保存源文件。

<全文完>

欢迎关注我的微信公众号：**码农在新加坡**，有更多好的技术分享。
![pic](/img/personal/qrcode_2.png)