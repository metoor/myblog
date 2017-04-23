---
title: 使用github+hexo搭建个人博客
categories: HEXO
tags:
  - HEXO
  - blog
date: 2017-04-22 15:22:38
---

## 概述
　　这个是本站的第一篇文章，我们该写点什么呢？很简单我们就写下本站是怎么搭建的吧。我们需要用到的框架是[HEXO](https://hexo.io/ "详情")： 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
<!-- more -->
## 搭建node.js环境
在安装HEXO之前需要先安装:

* [Node.js](https://nodejs.org/en/download/ "点我去下载")
* [Git](https://git-scm.com/downloads "点我去下载")

现在我们开始搭建Node.js环境，我这里以安装windows（win8.1）平台为例。点击上面的Node.js下载对应的版本

{% asset_img downloadnode.png  %}

1. 下载好后双击运行，跟着安装向导走就可以了，这里不多说。安装完成后正常情况下会自动设置好环境变量。
2. 点击开始-运行-cmd（win+R），打开dos，输入`node -v`检查Node.js版本：
{% asset_img doss.png  %}出现上述输出则表示你已经成功安装node.js
3. 使用cmd命令行输入`npm -v`来测试是否安装成功,如果成功会输出npm的版本号，这里就不放图片了。
4. 好了到这一步node.js已经装好了。详细教程可以参考[这里](http://www.cnblogs.com/zhouyu2017/p/6485265.html "详细教程")

## 安装git
点击上面的Git链接会打开如下页面：
{% asset_img downloadgit.png %}

1. 下载好后，双击运行安装程序，跟着向导安装就好了。
2. 关于git的一些基本使用命令可以参考这里[点我](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/ "快点我")

## 安装HEXO
1. 哈哈！！！终于到这一步了，其实这一步很简单，因为前面的安装好了这里用npm会非常简单哦。
	
```bash
	npm install -g hexo-cli
```

2. 安装完成以后输入 `hexo -v`出现如下界面则表示Hexo安装成功了:

	{% asset_img hexofinsh.png %}
3. 接下可以初始化我们的博客了，分别执行下面的命令（有没有很激动呢。。。）

```bash
	$ hexo init <folder>
	$ cd <folder>
	$ npm install
```
4. 依赖项装完以后可以在本地预览
5. 首先执行`hexo generate`生成博客的静态页面
6. 然后执行`hexo server`开启本地预览，在浏览器打开 http://localhost:4000/
{% asset_img finish.png %}

哈哈，有没有看到上述页面。到这里博客就创建好了。
## _config.yml配置
具体配置请参考[这里](https://hexo.io/zh-cn/docs/configuration.html "快点我")

## 部署到github
1. 注册github：部署到github自然需要有一个github账号啦。这个没什么好说的了。
2. 新建创库，这个用文字表达起来会略显繁琐，所以这里直接上图
{% asset_img git_1.png %}
{% asset_img git_2.png %}
3. 创建好仓库以后，我们需要打开_config.yml文件，添加如下内容
```deploy:
  type: git
  repository: https://github.com/yourname/yourname.github.io
  branch: master
```
4. 现在就差最后一步就可以部署到github了（很激动有没有，博客终于可以上线了，哈哈。。。）。now，执行下面的命令`$ npm install hexo-deployer-git --save`。最后一步部署命令`$ hexo deploy`。
5. 到这里本教程就完成了。赶紧打开浏览器输入http://yourgitname.gihub.io 看看你的成果吧。
 ps：第一次用MarkDown来写博客，写的不好莫怪哈。有错请指正。