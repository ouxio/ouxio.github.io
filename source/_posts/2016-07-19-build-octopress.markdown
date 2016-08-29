---
layout: post
title: "Octopress(一) 搭建octopress环境"
date: 2016-07-19 13:39:42 +0800
comments: true
categories: [octopress]
---
## <font color="#008000">#</font> Octopress介绍 ##
　　Octopress是一个基于Ruby的开源Blogging Framework，它不仅是一款优秀的静态化博客系统，也是一个本地化的博客系统。主要的优点如下：

1. 命令行操作
2. 纯文本写博客（图片，视频等）
3. 定制性高
4. 纯静态
5. 结合github的版本化管理
6. 迁移成本低
7. 简洁的Ruby框架
8. 使用Markdown语法 

### 工作流程与目录结构 ###
　　在下载安装完之后我们主要用到的几个文件夹为`source`和`public`，我们的源文件会存储在`source`文件夹下，然后通过`generate`命令生成静态的博客网页文件，存储在`public`文件夹下。这也是我们的一个工作流程。我们先有这样一个概念，往下会教怎么安装octopress。
![目录结构](http://7xwg81.com1.z0.glb.clouddn.com/octopress_01.png)

## <font color="#008000">#</font> 搭建环境 ##
　　由刚才的介绍可以知道，octopress是基于Ruby的一个框架，所以首先需要搭建Ruby的环境，但是由于国内某些原因（你懂的），使得搭建整个环境变得非常繁琐，甚至失败，所以我提供了搭建octopress所需要的所有工具安装包(只有64位的，32位的臣妾办不到呀)，下载链接在博客最下方，有需要的可以下载使用。
### 1.安装git ###
如果你的电脑已经有git的话就不用安装了，这里用的是1.9版本。打开`Git-1.9.5-preview20150319.exe`，选择路径，其余的步骤默认安装就好。关于git的安装百度一大把，这里不再详细说明。

![git_03](http://7xwg81.com1.z0.glb.clouddn.com/git03.png)

![git_04](http://7xwg81.com1.z0.glb.clouddn.com/git04.png)

安装完后，鼠标右键桌面空白地方，可以看到Git Bash..Git GUI什么的就是安装成功。

![git_success](http://7xwg81.com1.z0.glb.clouddn.com/gitbase.png)

### 2.安装Ruby ###
在下载完解压后，打开Ruby的安装程序`rubyinstaller-2.1.3-x64.exe`，选择路径，需要提下的是，在安装过程第二步中，必须要勾选第二个，把Ruby添加到系统路径中去。

![ruby_02](http://7xwg81.com1.z0.glb.clouddn.com/ruvy02.png)

安装Ruby还是相对简单的，接着就是安装DevKit。

### 3.安装DevKit ###
打开`DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe`程序，其实就是一个压缩包，打开解压到自己的路径下，时间有点久，耐心等候一下。

![devkit_01](http://7xwg81.com1.z0.glb.clouddn.com/devkit01.png)

### 4.连接DevKit与Ruby之间关系 ###
　　进入到DevKit文件夹下（注意必须是DevKit的安装目录下，因为我是安装在E：\DevKit下的，目录看自己定），鼠标右键打开Git Bash，输入

`ruby dk.rb init`

初始化dk.rb文件。执行完后，在操作目录下会生成一个`config.yml`的文件。用编辑器（Editplus或者Nodepad++都可以）打开确认Ruby的安装路径是否在文件末尾，如果没有就按这种格式`- E:/Ruby21-x64` 手动添加上去，注意一下格式。减号与路径之间有一个空格，如果是直接复制文件夹路径的，需要把反斜杠`\`改成斜杠`/`，比如`E:\Ruby21-x64`改成`E:/Ruby21-x64`，这也是一大坑之一。

![config](http://7xwg81.com1.z0.glb.clouddn.com/config.png)

确认Ruby的路径正确后，回到GitBash上，继续输入

`ruby dk.rb install`

执行安装。整个执行过程如下：

![ruby_devkit](http://7xwg81.com1.z0.glb.clouddn.com/ruby_devkit.png)

输出以上的`[INFO]`信息即为成功，如果输出其他乱七八糟的东西大多数是因为`cofig.yml`文件里面的Ruby路径出错，请仔细检查。

### 5.安装Octopress ###
　　这下进入正题，终于来到安装octopress这块了，如果把这一步安装成功，可以说整个安装环境就完成了一半。

　　打开[Octopress](http://octopress.org/)的官网，拉到最下面，然后点击`start here`，里面有octopress的安装教程，嫌麻烦也可以直接看这。

　　首先打开一个盘符，尽量不要在C盘，可以D盘或者E盘等，鼠标右键继续打开GitBash。输入

`git clone git://github.com/imathis/octopress.git octopress` 

把octopress克隆到我们的盘符下，稍等片刻。克隆成功后，就会在我们的操作目录下生成一个octopress文件夹。我们在GitBash上继续输入

`cd octopress`

进入到该目录，然后输入

`gem sources -a http://gems.ruby-china.org`

把gem的镜像源修改成国内的，注意这里的`http://gems.ruby-china.org`一定不能写错，没有`www.`，也不是`https`协议！我们再把gem默认的镜像源删掉，输入

`gem sources -r https://rubygems.org/`

这里的路径也不能写错。最后为了安全起见，输入`gem sources -l`查看源列表，确认只有一条`http://gems.ruby-china.org`镜像源。

![gem_sources](http://7xwg81.com1.z0.glb.clouddn.com/gem_sources.png)

修改完上面之后，还需要在octopress文件夹内找到并打开Gemfile文件，在第一行修改镜像源路径为`http://gems.ruby-china.org`，如下：

![Gemfile](http://7xwg81.com1.z0.glb.clouddn.com/Gemfile.png)

确认无误后，继续输入

`gem install bundler`

来安装bundler，输入命令后也许会出现一些怪异的现象(比如gitbash无响应了)，不要怀疑，相信自己是对的(然而笔者我ctrl+c停止执行，傻傻地去找无响应的原因了..)。原因上面说了，因为国内某些原因，视网络环境而定等待的时间偏长。安装完成后。继续输入

`bundle install`

来安装我们需要的工具，这里要注意，不要自以为是把`bundle`写成`bundler`（是的，说的就是我），这里安装的时间也偏长，这段时间可以去喝杯咖啡压压惊。

![Bundle_install](http://7xwg81.com1.z0.glb.clouddn.com/Bundle_install.png)

　　这里说下题外话，因为octopress是基于jekyll的(jekyll也是一个博客框架)，所以会安装jekyll的一些组件，还有就是sass是用来生成css样式文件的。感兴趣的可以再去了解。

　　以上都安装完后，环境就差不多了。我们一开始在介绍octopress时提到过，通过`rake generate`会在octopress\public的文件夹内生成博客网页。那我们就用`rake generate`命令测试下，有的可能会提示rake未安装，那么就先输入`rake install`安装一下，再执行以上命令。

`rake install`

`rake generate`

![generate_install](http://7xwg81.com1.z0.glb.clouddn.com/generate_install.png)
　　生成后，你也行会迫不及待地打开一个index.html文件查看，但不幸的告诉你并不是这样查看的。必须先要在本地建立一个服务器，输入

`rake preview`

提示一下，默认是选择4000端口的，如果你电脑的4000端口已经被占用，那么就会失败。在看到pid，port等信息后就表示成功。在浏览器上输入`localhost：4000`等待一段时间。

![rake_preview](http://7xwg81.com1.z0.glb.clouddn.com/rake_preview.png)

![firstblog](http://7xwg81.com1.z0.glb.clouddn.com/firstblog.png)
　　看到默认的网页My Octopress Blog就表示整个环境搭建成功。可能你会抱怨，为什么只是一个静态的网页要加载辣么长时间？下一篇将会讲解，并且说明octopress的配置以及如何生成一篇博客。

如果有错，或者有问题的欢迎在下方评论提出，谢谢。


----------


#####下载安装包：[百度网盘](http://pan.baidu.com/s/1pLH5Rtx)　　密码：knng #####

