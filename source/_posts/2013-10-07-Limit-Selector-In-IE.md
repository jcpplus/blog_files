layout: post
title: IE浏览器下,css选择器最大个数限制
date: 2013-10-07
category: 技术
tags: 
description: IE浏览器下,css选择器有个数限制...
---

## IE限制
今天听同学提到一个在ie8下的样式表问题:因性能优化需要将css样式表全部合并成一份，但是合并后的样式表在ie8下渲染不正常。同学通过一通查找，
~~发现ie系列下对css大小有288KB的限制~~。

<!-- more -->

以为这就是问题原因了。这个问题我也是第一次碰到= =，居然还有这种BUG，遂网络继续查找。


## 解决方案

然后，找到了这里 [IE中选择符的4095限制](http://dancewithnet.com/2009/09/10/ie-css-4095-limit/)，

直接转过来吧

>	去年曾总结了[IE对CSS样式表的限制和解决方案](http://dancewithnet.com/2008/04/22/a-solution-of-limit-of-style-tags-in-ie/)，中限制的第4条写道“一个CSS文件的不能超过288kb？”，这是一个疑问句，当时没有重现出来且参考来自Internet Explorer CSS File Size Limit。今天终于看到了IE在CSS上的另一个限制：IE中每个style标签或css文件的选择符个数不能超过4095。其实style属性也应该有这个限制，但是几乎不可能发生。这个限制在IE6、IE7和IE8中存在。
>	[请看IE关于4095个选择符限制的DEMO](http://dancewithnet.com/lab/2009/ie-css-4095-limit/)。

>	DEMO中的[style.css](http://dancewithnet.com/lab/2009/ie-css-4095-limit/style.css)，有4913个选择符，大小为554kb，但在IE中却在4095个选择符之后失效，所以说明IE的CSS文件不存在不能超过288kb的限制。

>	所以在IE中对style标签使用addRule方法和cssText属性添加样式时都可能会碰到这个限制，比如使用addRule方法添加第4096个选择符时会报“Invalid Argument”的异常。


## 结束
以上...权当备忘......
