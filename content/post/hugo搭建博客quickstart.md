---
title: "Hugo搭建博客quickstart"
date: 2018-05-15T10:49:04+08:00
draft: true
---

## 总揽

本文将介绍利用`hugo`来快速搭建一个简单的个人博客。有一下两部分功能：

> 1. 本地搭建: 先搭建一个博客，可以本地预览
> 1. 部署：将博客部署到`github`上，对外开放浏览

## 本地搭建

* 首先利用hugo命令行新建一个website目录（比如`blog`），用来放置博客文件。
	
	```
hugo new site blog
	```

* 为博客添加一个主题，主题会放置在 blog/themes 目录下。你可以在 [themes.gohugo.io](https://themes.gohugo.io/) 上查找你喜欢的主题，这些主题一般托管在github上，我们可以把它下载到themes目录下。  

	这里我们选择一个叫`beautifulhugo`的主题：
 
	```
	 cd themes
	 git clone https://github.com/halogenica/beautifulhugo.git beautifulhugo
	```

	然后设置默认主题为 beautifulhugo ：  

	```
	 cd ..
	 vim config.toml
	 theme = "beautifulhugo"
	```

* 利用hugo命令行在 content 目录中添加一篇博客文章，文章都是用`md`格式来编辑：  

	```
 	hugo new post/first.md
	```

	修改`post/first.md`的内容如下（todo）：
 
 	```
 	llllllll
 	```


* 利用hugo命令构建带 content 的博客，并在本地`localhost:1313`上启动 server：

	```
 	hugo server -D
 	```

* 浏览器打开`http://localhost:1313/`可以看到博客内容。  

至此本地搭建完成。


## 部署博客到github
 github页面 (`github pages`) 分两种：
 
 * `User/Organization Pages` (https://<USERNAME|ORGANIZATION>.github.io/)
 * `Project Pages`(https://<USERNAME|ORGANIZATION>.github.io/<PROJECT>/)

这里我们只介绍 `User/Organization` 类型的页面，也就是将博客页面托管到以下地址：
`https://<USERNAME|ORGANIZATION>.github.io/`
以下为步骤：
 
1. Ctrl+C 停掉本地server

1. 在github上新建一个repository（例如`blog`） 用来作为原始博客文件的远程仓库

1. 提交blog原始文件到github:

	```
   cd blog
   git init
   git add -f .
   git commit -m "first commit"
   git remote add origin git@github.com:<USERNAME>/blog.git
   git push -u origin master
	```
	
	后续如果博客有更新，再有修改需要提交，只需要执行：  
   
	```
   git add -A
   git commit -m "your commit message"  
   git push origin master  
	```

1. 再新建一个repository `<USERNAME>.github.io` 用来作为渲染后的博客文件的远程仓库

1. 将`<USERNAME>.github.io`作为 submodule 关联到 public目录：

	```
	git submodule add -b master git@github.com:<USERNAME>/<USERNAME>.github.io.git public
	```
	
1. 利用hugo命令行 build 生成渲染后的博客文件，文件的默认存放路径就是`public` 

	```
   hugo -D
	```

1. 提交`public`目录的渲染文件到`github`:

	```
	cd public
	git add .
	git commit -m "your commit message"
	git push
	```
	
1. 浏览器打开`https://<USERNAME>.github.io/`可以看到博客内容。

至此博客github部署完成。








