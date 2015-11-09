layout: post
title: 在Webstorm中执行sass编译
date: 2014-11-01
category: 技术
tags: 
keywords: sass
description: 正好碰到这个问题，gg一通之后觉得还是要随手一记吧。
---

#### Webstorm 大法好！

这个编辑器好强大哈哈。

知乎上有一篇专门说这个编辑器的好！只给[链接](http://www.zhihu.com/question/20936155)

<!-- more -->

*本篇假设机器环境已经安装好了ruby环境，sass环境等*

#### 官方文档

[官方文档](http://www.jetbrains.com/webstorm/webhelp/transpiling-sass-less-and-scss-to-css.html)

#### 目的

			myproject/
			|
			|-----assets/
			|           |-scss/
			|           |-----|-file.scss 
			|           |-style/
			|           |-----|-file.css

以上就是file.scss文件要输出到style目录下的file.css


#### 怎么操作

1： File >>  settings >> File Watchers， 增加scss的watcher

2： 主要更改这里

		Arguments: --no-cache --update $FileName$:$ProjectFileDir$\app\assets\style\$FileNameWithoutExtension$.css
		Working directory: $FileDir$
		Output paths to refresh: $ProjectFileDir$\app\assets\style\$FileNameWithoutExtension$.css    

3： 
其中的 `\app\assets\style\` 得根据自己项目的实际情况更改目录


#### 结尾
截图好麻烦啊


-------
update 2014.11.12

#### 补充

1： 这个参数可为空。

2： 输出样式支持scss输出参数。 在`Arguments`项的 --no-cache 之后写 `--style compressed`
