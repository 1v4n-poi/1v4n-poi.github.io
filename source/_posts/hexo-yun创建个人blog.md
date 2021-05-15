title: Hexo+Yun创建blog的碎碎念
author: 1v4n-poi
tags:
  - 教程
  - Hexo
  - Yun
categories:
  - 网站搭建
date: 2021-05-15 10:56:00
---
# Hexo+Yun的碎碎念

## 写在前面

本文内容主要是自己用hexo搭建个人blog时遇到的一些**小问题的解决方案**和若干**useful tips**。针对的是已经完成了git repo的建立，以及本地hexo环境部署工作的零基础/弱基础读者（同时也是在下_(:з」∠)_）。OK, Let's get it！

<!--more-->

## 从零开始的参考资料

本站部署Hexo时主要参考了知乎用户Crystal分享的[相关教程](https://zhuanlan.zhihu.com/p/60578464)，设置Hexo时主要参考了Hexo的官方中文[Manual](https://hexo.io/zh-cn/docs/)。Yun主题的相关部署与设置参考了[云游君](https://www.yunyoujun.cn/)大佬的Yun主题使用手册（链接是左边的小齿轮）。如果你喜欢本站，希望从零开始搭建的话可以参考这些链接，里面都有很详细的操作步骤。

## 小问题和解决方案

以下所有建议均是在网络环境正常的条件下进行的，如果出现连接问题请优先解决网络环境问题。

### 有关github repo的命名

虽然网上的说法各异，但这里推荐repo的名字与你的github用户名**完全一致**，对新手而言这可以避免后面的诸多问题。

### 有关本地Hexo文件夹下_config.yml文件的depoly部分修改

在Crystal分享的操作中，修改设置为

	deploy:
   	type: git
   	repository: git@github.com:用户名/用户名.github.io.git
   	branch: master
其中repository简写为repo也没有问题，后面的链接根据你的网络情况可以选择使用ssh链接或者https的[github链接](!https://cdn.jsdelivr.net/gh/1v4n-poi/1v4n-poi.github.io@hexo/images/20210515/1.jpg)。branch默认为master，最好在github中设置当前repo的默认branch为master（我一开始就设置了，没有测试过不设置的情况，了解的小伙伴可以在评论区分享一下）。此外，在branch后面还可添加message命令，用以本次部署的简单说明。

### 为什么blog本地调试正常，部署成功后网页显示404？

可能和你的网络（魔法）状态有关，第一次部署速度时速度也会比较慢。玄学如我的的话可以试试更换上面repo的链接试试，或者多hexo d几次（后面就会提示nothing to commit, working tree clean）。

### 为什么部署成功，进入网页后排版错乱？

与浏览器缓存有关，清除缓存后刷新即可。

### 为什么本地blog修改后重新部署，网页没有变化？

hexo clean后再hexo g -d（generate和deploy一起进行）试试。

### 主页的about链接导向404？

为了设置个人博客介绍页面，这里建议安装Hexo Admin插件，在blog根目录下执行
	
    npm install --save hexo-admin
    hexo s

之后就可以通过 http://localhost:4000/admin/ 进入管理页面了。随后在Pages分栏中创建about page，用markdown语法编辑内容就可以。

### 主页文章底端的链接显示不正常？

原因是Hexo目录下_config.yml文件中url没有正确设置，这里设置为`https://username.github.io/`即可。


### 有关Yun的小问题

#### 网页中文章的Tags/Categories分类导向404？

这里应该算是自己的疏忽（汗），考虑到前面创建about页面一切正常，这里也有样学样创建了tags和categories页面，但是网页却导向了404。。。

后来look back到Yun的手册，发现是缺少了`hexo-generator-tag`和`hexo-generator-category`，可以通过`npm ls --depth 0`查询安装情况。

用`npm install hexo-generator-tag`以及`npm install hexo-generator-category`完成安装，具体设置可参考Yun主题手册中[页面配置](https://yun.yunyoujun.cn/guide/page.html#%E6%96%87%E7%AB%A0)部分。设置完成后再次部署即可实现正常功能。

### ....

后续遇到的问题和解决方案我会持续update，毕竟咱也是新手_(:з」∠)_。

## 一点useful tips

### 图片链接

引用储存在github repo内的图片建议使用`https://www.jsdelivr.com/`，国内访问速度比较优秀。

### 关联远程仓库与建立源代码分支

参考云游君大佬的[教程](https://www.yunyoujun.cn/share/how-to-build-your-site/)2.5小节。方便备份和多台电脑间操作。


