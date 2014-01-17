---
layout: post
title: "使用octopress部署github博客"
date: 2013-09-14 15:45
comments: true
categories: 
---

* ##安装octopress
###使用这个网址：[安装octopress](http://voodeng.com/blog/2012/09/02/octopress-on-github/)
###在使用过程中由于网络环境的问题，所以需要更换ruby的源：具体请看[淘宝源](http://ruby.taobao.org/)
* `git clone git://github.com/imathis/octopress.git yourname.github.io`
* `cd yourname.github.io`
* 修改Gemfile和Gemfile.lock文件中的`源`，国内网络环境不稳定。
* `bundle update` 可能需要 `bundle install`安装所需要的
* `rake install` 安装默认的主题
* 修改_config.yml文件中，google analystic的id 和disqus的评论的名字等
* `rake gen_deploy`发布空的博客的系统。你的远端的blog中有文章等内容的时候，你需要看下面的内容

* ##有了内容怎么办
* 在_deploy文件夹下使用`git pull origin master`，获取远端内容（这时git的源其实已经成为了你的yourname.github.io中的master分支了，在yourname.github.io文件夹中内容推送到远端的source的分支了，两个文件夹的分支是完全不同的）
* 然后在yourname.github.io文件夹下再使用`rake gen_deploy`