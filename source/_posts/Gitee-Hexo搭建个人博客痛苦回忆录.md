---
title: Gitee+Hexo搭建个人博客痛苦回忆录
date: 2021-10-20 16:02:37
tags: Hexo
---

{% asset_img image.jpg %}

### 起始

因为正在实习，所以打算记录自己的实习经历和以后的学习记录，所以搭建了博人博客来记录，因为以前只接触过采用Hexo搭建博客的方法，所以这次采用了Hexo重新搭建个人博客。由于国内访问Github的速度非常慢，所以这次部署到国内的Gitee上。不过经过这次搭建的经历，让我实打实地感受到了Hexo在采用社区主题搭建博客的痛苦，先讲我的搭建过程吧。

<!--more-->

### 安装环境

首先需要nodejs(js依赖)[Nodejs官网 ](https://nodejs.org/en/)还有[Git 官网](https://git-scm.com/)，这两个环境依赖自行安装下载，网上也有很多教程

```
git --version
npm --version                 #可以查看git，npm的版本
```

下图是我的版本

{% asset_img gitnpmversion.jpg %}

然后是开始安装Hexo

``` 
npm install -g hexo 		# 通过npm安装hexo
# -g 指定全局安装，可以使用hexo命令
```

如果你的下载非常慢的话，可能是镜像源是国外，可以采用以下命令换为国内源

```
npm config set registry https://registry.npm.taobao.org		#配置国内的镜像源
npm info hexo				# 测试查看hexo的安装信息，是否是taobao.org的源
```

{% asset_img npm.jpg %}

安装测试完成之后就可以开始使用Hexo初始化一个博客了，在命令行输入一下命令，文件夹名称随意起，这里blog是我自己方便查找，后续部署以及写博客需要继续使用这个文件夹

```
hexo init blog		# 初始化创建，会再桌面创建blog文件夹
cd blog				# 进入blog目录
npm install			# 进一步安装hexo所需文件
```

然后在这个文件夹下输入以下命令初始化Hexo

```
hexo clean			# 清除所有记录
hexo generate		# 生成静态网页
hexo server      	# 启动服务
###############################可以简写成以下
hexo clean
hexo g
hexo s
```

然后使用浏览器访问`localhost:4000/`这个是在`hexo s`命令提供的本地网址和端口号

{% asset_img hexo初始化.jpg %}

### 主题配置

默认的主题我个人看着非常一般，采用的话是Hexo社区的next主题，[next主题的源码](https://github.com/iissnan/hexo-theme-next/)以及[Next官网](http://theme-next.iissnan.com/getting-started.html)，这个主题目前文档是比较丰富的，方便我们进行修改。

首先我们到next在github的网页，往下找到稳定版(其他版本可能存在bug，我没有采用)

{% asset_img next1.jpg %}

可以点击蓝色部分跳转，也可以按照文档的命令行进行下载，这里我选择的是浏览器下载的方式

跳转页面之后选在ZIP格式下载

{% asset_img next2.jpg %}

然后将压缩包解压并将文件名改成next，粘贴到blog的themes下，如图

{% asset_img next3.jpg %}

然后使用记事本或者其他编辑器打开blog文件夹下的`_config.yml`文件，这里博主采用的是VsCode打开，(VsCode是一个功能强大的编辑器，丰富的插件能让程序员敲代码更舒适)。

在`_config.yml`中找到如图这行将`landscape`改为`next`并保存，如图

{% asset_img next4.jpg %}

！！！需要注意的是theme的`:`后面必须要有一个空格，否则会报错

还有一点如果出现`{% extends ‘_layout.swig‘ %} {% import ‘_macro/post.swig‘ as post_template %}`的报错信息的话，应该是安装的版本问题，新版的hexo将swig删除了，我也是搜索社区才找打解决的方法，执行一下命令，自己手动安装swig [解决方法地址](https://blog.csdn.net/qq_39898645/article/details/109181736)

```
npm i hexo-renderer-swig
```

之后就重启hexo服务了

```
hexo clean
hexo g
hexo s
```

{% asset_img next5.jpg %}

当然单是这样还不够，我想弄一些其他的插件和样式，如果觉得这样就可以了的话可以直接跳到后续部署到Gitee上的操作

### 主题样式修改和插件安装

#### 主题样式

在themes文件夹中next文件夹下的`_config.yml`(主题的配置文件)，默认模板是Muse，我选择的是Gemini，仍然要注意`:`之后要有一个空格，不然会报错，保存

{% asset_img theme1.jpg %}

图省事，我们再更改剩余一部分样式再重启hexo，在blog文件夹下的`_config.yml`

{% asset_img theme2.jpg %}

以及博客的菜单

{% asset_img theme3.jpg %}

对应首页，关于，分类，归档

对应的是博客的标题，博客最下面的博客作者著名，以及博客是的的语言，简中为`zh-Hans`，仍然注意`:`之后有空格，保存

接下来重启hexo服务就可以看到我的博客的模板样式了

{% asset_img theme4.jpg %}

#### 插件

网易云音乐插件，到网易云音乐官网找到你喜欢的歌曲

{% asset_img theme5.jpg %}

{% asset_img theme6.jpg %}

复制这段代码，粘贴到 themes -> next -> layout -> _macro -> sidebar.swig ，粘贴到合适的位置，我是放在回到顶部按钮的上方

{% asset_img theme7.jpg %}

回到顶部按钮默认是右下角，这里我是修改到左边侧边栏

{% asset_img theme8.jpg %}

修改方法为在next的`_config.yml`下找到`b2t`，将false改为true即可，scrollpercent表示显示百分比

{% asset_img theme9.jpg %}

Live2D 看板娘

[Hexo Next 添加萌萌的宠物live2d ](https://vonsdite.github.io/posts/fbd1f97f.html) 这篇教学非常的简单明了

之后就可以开始部署在Gitee上了。

### 部署到Gitee

首先查看自己的个人空间地址，如果没有就设置一个，记住这个地址的后缀

{% asset_img gitee1.jpg %}

右上角新建仓库

{% asset_img gitee2.jpg %}

仓库命必须和个人空间地址后缀一致

{% asset_img gitee3.jpg %}

其他设置默认即可，然后打开新建的这个仓库，辅助仓库地址

{% asset_img gitee4.jpg %}

找到blog下的配置文件`_config.yml`，找到仓库repo接口更改为前面复制的仓库地址，然后保存

{% asset_img gitee5.jpg %}

在blog文件夹下执行以下命令，先安装一个hexo上传git的插件

```
npm install hexo-deployer-git --save	# 安装git插件
git config --global user.email *********@qq.com	# 设置gitee邮箱（gitee的注册邮箱）
git config --global user.name '****'			# 设置用户名（git的注册昵称）
hexo deploy	# 上传到gitee
#############
hexo d      #hexo deploy简写
# 在上传时，需要再次输入gitee的注册邮箱作为username，账户密码作为password
```

这时候我们的博客代码就上传到gitee上了，之后就是部署，找到仓库的Gitee Page网页解析服务

{% asset_img gitee6.jpg %}

刚开始需要实名认证，而且人工审核，估计需要一天时间，审核通过后就可以部署了

{% asset_img gitee7.jpg %}

点击更新，更新完成后，再点击提供的网站地址，就可以看到我们的博客部署到服务器上了

到此为止就是博客的部署以及部署过程中踩得坑，后续还有关于写博客存在的一些坑。



​		_来投一枚硬币 祝你欢天喜地 来投两枚硬币 手留余香茉莉 感谢你们硬币 使我更有动力 给我充足打气  ——济南屁王_









