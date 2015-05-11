title: "hexo搭建在gitpage上的博客重新搭建"
date: 2015-05-11 21:25:59
categories: 技术
tags: hexo
---
    在自己的机子上使用了hexo搭建了gitpage，并且代码提交到了github，突然有一天有需要重新clone处理一下搭建的gitpage，这个时候我们需要的是再原有的基础之上写文章，什么都不变。

<!--more-->

为了这个目标，需要了解github的显示原理或者路径，这样才能更好的理解处理内容。

## master 分支
在github中的，只有master分支的内容才能显示到你访问的站点上，所以在使用hexo时，public的文件夹，也就是你的博客生成后的内容的文件夹，这个文件夹使用了clone远端服务器上master分支，这样保证了hexo能自动生成到public文件夹，并且提交到远端服务器上的master分支上。


## 保存个性化的信息和原文章的备份
除了master分支外，还需要把编写的文章的txt文本和主题的个性化、模板的个性化设置保存起来，这个分支是准备工作的内容，在此分支下就是hexo的基础环境的一个目录结构，当然这个时候就算pull下来也是无济于事的。


以上的两个分支都是在同一个blog版本库上的，好了，现在举例说明一下，怎么做。

## 换机子或者其它的修改来从新搭建gitpage

### git hub的内容获取
  > git clone https://github.com/XX/XX.github.io youblogfoldername
  > git checkout source //我的保存环境的分支叫做`source`,这块根据你的环境决定
  > git pull
  > cd youblogfoldername
  > git clone https://github.com/XX/XX.github.io public //保存成public名字的文件夹
  > git pull


以上就是把版本呢库拖下来的命令，根据自己的需要进行相应的修改，现在版本库有了，但是还是没有hexo的运行环境，请看下面：

### hexo的运行环境搭建（以前已经安装过hexo）
首先要初始化一下次
  > hexo init youblogfoldername  //注意，这块的命令是在youblogfoldername的父目录中执行的。

然后，再在`youblogfoldername`的目录中执行如下操作：
  > npm install

以上呢，就是hexo环境搭建。这个时候其实博客的内容配置还是有问题的，因为hexo会覆盖原有的本地文件夹同名的内容，所以需要再进行一次回滚操作
  > git checkout .

好了，博客重新搭建好了，跟以前一样的操作。

##总结
github真是不错，能恢复这些内容，以前自己使用octopress的就是搞不清这两个分支的概念自己觉得很憋屈，于是没有再更新，前段时间是想在搭建一下，于是找到了hexo，这个使用方便的搭建工具，官方网站的内容还是比较详细的。
