title: 使用fiddle调试移动端页面
date: 2015-07-21
categories: 技术
tags: fiddle
description: fiddle是前端调试神器之一。要使用fiddle调试移动端页面，只要对fiddle做简单设置即可。
---

fiddle是前端调试神器之一。要使用fiddle调试移动端页面，只要对fiddle做简单设置即可。

# 1
Tools》》Fiddle Options
![进入fiddle Options]({{BASE_PATH}}/img/fiddle4/1.png)

# 2 
Connections，勾选`Allow remote computers to connect`,
可以看到端口号默认为`8888`

![勾选选项]({{BASE_PATH}}/img/fiddle4/2.png)

# 3

设置好，保存之后 ，记得 **重启** fiddle。

好了，结束！

哦，对了。设置完了后其实是利用*请求重定向*来调试代码，

##请求重定向(AutoResponder)

所谓请求在我们前端就是一些基本的css，js，图片等请求，重定向是指页面请求资源文件替换成其他需要替换成的文件。

比如我们现在需要调式线上一个js或者css文件等，我们可以使用fiddler捕获这个文件的请求，然后复制线上一份文件(比如JS或者css)代码放到本地，然后在本地的文件修改完后，替换线上的文件来调式，当一切都好了话，我们可以直接把代码提交到服务器上即可!
*此乃利器*

# 4 
没有终点~

这是一些参考，一些更加高级的使用方法
[http://web.jobbole.com/82706/](http://web.jobbole.com/82706/)
[http://web.jobbole.com/82710/](http://web.jobbole.com/82710/)
[移动端前端开发调试](http://yujiangshui.com/multidevice-frontend-debug/)
