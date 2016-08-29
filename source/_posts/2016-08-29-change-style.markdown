---
layout: post
title: "Octopress(三) 个性化博客"
date: 2016-08-29 21:51:09 +0800
comments: true
categories: [octopress]
---
　　　　这几个星期都在忙学校的项目，所以博客这边就耽搁了，实在是不好意思。看着有一天空就赶紧把octopress系列的博客更新一下。
## <font color="#008000">#</font> 添加评论插件 ##
　　在自定义之前先要要了解一个主配置文件，就是在occpress文件夹下的 `_config.yml` 文件。打开这文件观察一下，可以发现有一些基本的配置属性，比如博客的title，subtitle等。我们可以根据自己的喜好来修改这些属性，其中 `simple_search` 这个属性中的google搜索在国内并不友好，所以可以改成其他的搜索引擎，比如百度。

![config01](http://7xwg81.com1.z0.glb.clouddn.com/config01.png)

还有一些常用的功能开关。

![config02](http://7xwg81.com1.z0.glb.clouddn.com/config02.png)

　　在上诉的主配置文件中，有twitter、google..等待其他功能开关，细心的同学可能看到名为disqus的功能开关。是的，其实它就是octopress的默认评论插件，只是在国内也是相当不友好。我们可以把它修改成国内比较好用的评论系统，比如多说等。

　　OK，想自定义博客首先要修改`_config.yml`主配置文件。刚我们说了，disqus是默认的评论系统，但国内并不能用。我们可以在文件末尾根据格式创建一个评论开关的名字。如下：

![duoshuo01](http://7xwg81.com1.z0.glb.clouddn.com/duoshuo001.png)

然后打开 `octopress\source\_layouts\post.html` 文件，把默认的disqus开关修改成我们刚创建的评论开关，具体在文件哪个部分可以看行号哈~

![duoshuo02](http://7xwg81.com1.z0.glb.clouddn.com/duoshuo002.png)

根据以上修改的 `include post/duoshuo_comment.html` 这个路径相信可以猜到，我们要在 `octopress\source\_includes\post` 文件夹下新创建一个 `duoshuo_comment.html` 的文件来装载我们自己的评论插件代码。

　　想要使用多说评论插件首先要在多说注册一个账号。百度多说进入官网，可以用QQ什么的直接登录，然后点击开发者文档，滚到下面，在左侧的安装帮助里点击"discuz通用代码"。在【准备工作】中，点击"获取多说通用代码"的链接。就进入创建站点的页面，输入基本信息。创建完站点后，导航栏会多出一个"后台管理"的标签，里面会有一个刚创建的名称。再点击进去，在左侧点击"工具"，就会看到一段代码，我们直接复制过来，粘贴到我们刚创建的html文件中。最后把需要修改的地方修改过来。

![duoshuo03](http://7xwg81.com1.z0.glb.clouddn.com/duoshuo03.png)

　　如果以上流程没有出错的话，重新生成网页，再执行预览。点进一篇博客后，应该就可以看到多说评论区域。

## <font color="#008000">#</font> 添加社会化分享 ##
　　添加社会化分享和添加评论插件过程差不多。首先在 `_config.yml` 主配置文件添加一个分享的开关。

![share01](http://7xwg81.com1.z0.glb.clouddn.com/share01.png)

然后打开 `octopress\source\_includes\post\sharing.html` 文件，我们可以发现，其实它已经有默认的分享插件，只是和评论插件一样，在国内不友好。我们可以不理会，直接在下面再添加自己的分享开关。如下：

![share02](http://7xwg81.com1.z0.glb.clouddn.com/share02.png)

是的，接下来的操作和操作评论插件一样，在 `octopress\source\_includes\post`
文件夹下，新创建一个 `jia_share.html` 的文件。那么里面的内容呢？打开 <http://www.jiathis.com/> ，选择自己想要的样式，然后复制代码到 `jia_share.html` 保存就完成了。

　　最后重新生成网页，执行预览，点进一篇博客中去，查看效果。在刚添加的评论上应该就可以看到分享按钮了。

## <font color="#008000">#</font> 自定义导航栏 ##

　　自定义导航栏相比之前两个比较简单。打开 `octopress\source\_includes\custom` 文件夹，找到 `navigation.html` 文件，发现就只有几行代码，而且还可以看到非常熟悉的两个关键字，Blog和Archives。这不就是每次打开博客首页时，导航栏上的两个按钮吗。看到这就嗨心了，直接复制一行，然后修改导航名字和链接。但是链接到哪去呢？还记得在第二篇介绍octopress时新建的单页面吗？（不记得的返回去看）在新建单页面后会在 `octopress\source` 新生成一个文件夹，里面只包含一个 `index.html` 的文件。此时我就可以应用到导航栏中。修改如下：

![navigation01](http://7xwg81.com1.z0.glb.clouddn.com/navigation01.png)

最后重新生成网页，执行预览。打开就会发现在导航栏中多出一个导航按钮，点进去，就是我们新建的单页面。


## <font color="#008000">#</font> 自定义主题 ##

　　即使修改了以上的一些简单的配置后，你还意犹未尽。觉得这个博客简直是太TM难看了，对比其他人的博客真是弱爆了。别急，让我们来一个大修改，让你的博客变的与众不同。Octopress提供了很多不错的主题样式供我们选择，但是必须说明的是，在应用这些主题之前最好先备份一下你的octopress文件夹。因为在应用主题之后它会覆盖掉我们之前上面所做的所有修改，当然，不包括博客内容，只是样式。

　　在使用新主题前，我们可以发现在 `octopress` 下有一个 `.themes` 的文件夹，懂英语的人都明白这是主题的意思。打开发现，里面只有一个classic的文件夹。是的，这就是我们现在应用的主题（是不是很难看(¬_¬)..）。好了，那我么就换掉这个主题。打开gitbase，进入到octopress文件夹内，然后输入以下代码：

`git clone git://github.com/gluttony/object-octopress-theme.git .themes/object `

然后等待下载主题。解释一下，`git clone` 这不用说了吧，就是克隆。 `git://github.com/libingcun/libingcun-octopress-theme.git` 这段就是克隆源的地址 `.themes/libingcun-octopress-theme` 就是克隆到哪，即目标地址。下载完毕后，会在 `.themes` 文件夹下新生成一个 `libingcun-octopress-theme` 主题文件夹,其实就是主题的名字。

接着，在gitbas中再执行

`rake install['themeName']`

输入以上命令后，等半天没反应...输入 `y` 确认继续安装。

完成后，再重新生成网页，执行预览查看，就会看到新的主题博客啦！！但是之前设置的评论和分享都没了。如果你想有评论和分享，那么请再做一遍上面的步骤。呵呵，我就是故意把主题放在最后讲的。(微笑脸.jpg)

好吧，为了弥补过错。我分享一个主题集吧~大家可以在里面找到漂亮的主题哟。
<https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes>

下一篇将讲解如何把自己的博客放到外网上，供其他人访问。

如果有任何问题，欢迎在下方评论提出，谢谢。



