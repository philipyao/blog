---
title: "Hugo搭建博客quickstart"
date: 2018-05-15T10:49:04+08:00
draft: true
---

本文将介绍利用hugo来快速搭建一个简单的个人博客。

 第一步：先在本地搭建一个博客，可以本地预览
 第二步：将博客部署到github上，对外开放浏览

## 本地搭建

 0. 首先利用hugo命令行新建一个website目录（比如blog），用来放置博客文件。

 hugo new site blog

 1. 为博客添加一个主题，主题会放置在blog/themes目录下。可以在 themes.gohugo.io 上查找你喜欢的主题，这些主题一般托管在github上，我们可以把它下载到themes目录下。
 这里我们选择一个叫beautifulhugo的主题：
 cd themes
 git clone https://github.com/halogenica/beautifulhugo.git beautifulhugo

 然后设置默认主题为beautifulhugo：
 cd ..
 vim config.toml
 theme = "beautifulhugo"

 2. 利用hugo命令行在content中添加一篇博客文章，文章都是用md格式来编辑：
 hugo new post/first.md

 修改post/first.md内容如下（todo）：


 3. 利用hugo命令构建带content的博客，并在本地 localhost:1313 上启动server：
 hugo server -D

 4. 浏览器打开 http://localhost:1313/ 可以看到博客内容。至此本地搭建完成。


## 部署博客到github上
 github页面分两种：
 User/Organization Pages (https://<USERNAME|ORGANIZATION>.github.io/)
 Project Pages (https://<USERNAME|ORGANIZATION>.github.io/<PROJECT>/)

 这里我们只介绍User/Organization类型的页面
 
0. Ctrl+C 停掉本地server

1. 在github上新建1个repository: blog 用来作为原始博客文件的远程仓库

2. 提交blog原始文件到github
   cd blog
   git init
   git add .
   git commit -m "first commit"
   git remote add origin git@github.com:<USERNAME>/blog.git
   git push -u origin master

   后续如果再有修改需要提交，只需要执行：
   git add .
   git commit -m "your commit message"
   git push


4. 再新建一个repository：<USERNAME>.github.io 用来作为渲染后的博客文件的远程仓库

5. 将<USERNAME>.github.io作为submodule关联到public目录：
	git submodule add -b master git@github.com:<USERNAME>/<USERNAME>.github.io.git public

6. 利用hugo命令行build生成渲染后的博客文件，文件的默认存放路径就是public
   hugo -D


7. 提交public目录的渲染文件到github
	cd public
	git add .
	git commit -m "your commit message"
	git push

8. 浏览器打开 https://<USERNAME>.github.io/ 可以看到博客内容。至此博客github部署完成。








