---
title: 搭建你的第一个博客
description: 使用Hugo Stack主题搭建你的第一个博客
image: keila-hotzel-tJtUvIG3vPI-unsplash.jpg
date: 2025-04-03 00:00:00+0000
categories:
    - 博客搭建
tags:
    - 博客搭建
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

# 搭建你的第一个博客

## 安装Hugo

> 说实话，我也是刚刚才会搭建Hugo博客，然后就来教别人了。这个的感觉就很像这个博主[失踪的博客](https://blog.reincarnatey.net/2023/build-hugo-blog-with-stack-mod/)的开头一样。

以windows操作系统为例，我们需要先下载Chocolatey软件包管理器（[点击此链接前往下载地址](https://chocolatey.org/install)），然后复制此行命令。

![](/choco.png)

按住`win`+`X`键，选择以管理员模式运行powershell，运行此命令。

> 官方说不要用Windows Powershell，要用Powershell，说它们是两个不同的东西，但是我用了Windows Powershell却并没有出现任何的报错。目前还不清楚这其中的原因。

然后执行安装hugo的命令

``` sh
choco install hugo-extended
```

安装完以后可以用下面的命令查看hugo版本，检测是否安装成功

```sh
hugo version
```

## 安装Hugo Stack主题

Hugo的主题是需要自己选的。在Hugo的众多主题里面，我特别喜欢Stack的Card-Style风格，所以我就使用了Hugo Stack主题。我们可以前往Github下载Hugo Stack的[模板](https://github.com/CaiJimmy/hugo-theme-stack-starter)，然后自己修改。

修改好了后在文件夹下运行此命令

```
hugo server
```

他会提示你访问一个链接，默认是http://localhost:1313/。如果能看到的话就说明你成功了

## 部署到Github

你下好了这个模板后，自带Github的workflow action部署文件，基本上不用管什么，作者算是有心了。但是你可能还需要修改一个地方，如果你的默认分支是其他的不是master，比如是main，你应该把此文件`.github/workflows/deploy.yml`中的关于分支部分的代码改为如下所示的代码

```yml
on:
    push:
        branches: [main]
    pull_request:
        branches: [main]
```

然后把你的hugo push到你的Github仓库上

## 部署Giscus评论系统

确保你的项目开了Discussions功能，然后前往giscus官网，按照他的提示输入。你可以参考Vitepress部署Giscus的方法。这里不在赘述了，网上很多教程。获取到相应的参数就行

然后找到这个文件`/config/_defalut/params.toml`，把comment项改为

```toml
[comments]
enabled = true
provider = "giscus"
```

然后把giscus那项的参数都填上，不要忘记在加上enabled = true，如下

```toml
[comments.giscus]
enabled = true
repo = "euuen/euuen.github.io"
repoID = "R_kgDONltvFw"
category = "Announcements"
categoryID = "DIC_kwDONltvF84CovmA"
mapping = "pathname"
theme = "preferred_color_scheme"
lang = "zh-CN"
loading = "lazy"
reactionsEnabled = 1
emitMetadata = 0
```

然后，恭喜你，你也有了自己的评论系统了！！

>Photo by <a href="https://unsplash.com/@keilahoetzel?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Keila Hötzel</a> on <a href="https://unsplash.com/photos/gray-and-black-laptop-computer-tJtUvIG3vPI?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>
