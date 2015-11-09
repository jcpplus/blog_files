layout: post
title: requirejs
date: 2015-06-20 09:17:17
categories: 技术
tags: js
description: 基础的针对requirejs的记录，备忘 http://anjia.github.io/2015/04/17/fe_requireJS/
---

# 解决的问题

早期，所有的 JS 代码都写在一个文件里，只要加载这一个文件就可以了。后来，代码越来越多，就分成了多个文件，再依次加载。诸如：

```js
<script src="1.js"></script>
<script src="2.js"></script>
<script src="3.js"></script>
<script src="4.js"></script>
<script src="5.js"></script>
<script src="6.js"></script>
```
以上代码会依次加载多个 JS 文件。但有缺点：

1.加载时会阻塞浏览器渲染网页。文件越多，网页失去响应的时间就越长。
2.当 JS 文件间存在依赖关系时，需要人工严格保证加载的顺序。当依赖关系复杂的时候，就会难以维护。

为了解决以上这两问题，requireJS 诞生了。
1.实现 JS 的异步加载，避免网页失去响应。
2.管理模块间的依赖性，便于代码的编写和维护。

# 使用
## 主页面

在[官网](http://requirejs.org/docs/download.html)下载requireJS的最新版本，在页面中引用它。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>requireJS 入门小练习</title>
</head>
<body>
    <!-- data-main 属性指主模块|入口模块，主模块是整个网页的入口代码，类似C语言的main()函数 -->
    <script src="require.js" data-main="js/main.js"></script>
</body>
</html>
```
只需用 `script` 标签引入 `require.js` 即可，其他的文件模块都不再使用 `script` 标签引入

## 主模块 
主模块 main.js
常见的情况是主模块依赖其他模块， 这时就使用AMD 规范定义的require()函数

```js
require.config({
    baseUrl: 'js/', 
    paths: {
        jquery: 'jquery'
    }
});
require(['jquery', 'math'], function($, math){
    alert($().jquery);  //弹框显示当前jQuery的版本
    var ele = math.sum(4,5);
    console.log(ele);
});
```

main.js 中有两个函数调用

require.config()

配置一些参数，它将会影响到 requirejs 库的一些行为。[常用的配置](http://requirejs.org/docs/api.html#config)有`baseUrl`，`path`：

（1）baseUrl 来配置模块根目录：若没写-则path的路径默认是和 main.js 同层；一旦写了则是相对于 index.html；当然也可是绝对路径
（2）path 属性指定各个模块的加载路径：其中jquery是模块的名字，值是路径（它的根路径可由baseUrl来定义）

require() 有两个参数

（1）第一个参数是一个数组，表示所依赖的模块名，是字符串类型
（2）第二个参数是回调函数，加载的模块会以参数形式传入该函数，从而实现在回调函数内部使用这些模块
require() 异步加载各个模块，浏览器不会失去响应。它指定的回调函数，只有当前面的模块都加载成功后，才会运行。解决了依赖性问题。


说明：

如果 require.config() 里的 baseUrl
（1）baseUrl 没有定义，则默认是和主模块 main.js 同目录
（2）baseUrl 的值是空字符串’’，则默认是和主页面 index.html 同目录
如果 require() 里的模块名在 require.config() 的 paths 里没有定义，比如上例中的 ‘math’，则默认路径是和主模块 main.js 同目录，且默认文件名字是 模块名.js。


在 require 中是以模块名字为唯一标识的。【符合预期嘛，减少相同模块的重复加载。但使用不当会造成文件的覆盖】
（1）主模板依赖了 jquery，如果子模块也依赖 jquery，且模块的名字和主模块里的相同，都是’jquery’，那么整个程序就只加载其中一个，且只加载一次。具体加载谁，依据依赖顺序（因为在子模块里也可以重新设置 require.config() 去配置）。此例会优先加载主模块里的 jquery。
（2）如果不同的子模块都用到了 cookie 插件，但 cookie 里的代码不同。在使用时，请将两个模块名字赋成不同的值，否则会造成 js 的相互覆盖。

## 其他模块

math.js的内容 

```js
define(function($){
    function sum(a, b){
        return a+b;
    }
    return {
        sum: sum
    };
});
```

由于 requireJS 加载的模块是采用的 AMD 规范，所以要用 requireJS 来加载的模块也必须按照 AMD 的规范来写。必须采用特定的 define() 函数来定义。详情参考[AMD模块的写法](http://anjia.github.io/2015/04/17/fe_requireJS/#AMD模块的写法)。


# 运行结果

文件的目录结构：
![rq]({{base_path}}/img/requirejs_base/1.png)

当我们在浏览器中打开 index.html 页面时，可以看到除了 require.js 外，main.js、jquery.js 和 math.js 也都请求了。后三个正是通过 require 请求的。

![requirejs]({{base_path}}/img/requirejs_base/2.png)

这是一个很简单的例子，使用 requireJS 动态加载 jquery.js 和 math.js，知识点：

data-main 属性：指出主模块
require.config() 自定义模块的加载行为
require() 异步加载各个模块
define() 定义一个函数类型模块。requireJS 的模块可以是JS对象、函数、或其他类型（CommonJS/SeaJS则只能是JS对象）
说明：
requireJS 要求每个模块都是一个单独的 js 文件，这样，如果加载多个模块，就会发出多次 HTTP 请求，会影响网页的加载速度。所以，requireJS 提供了优化工具，当模块部署完毕后，可以用这个工具将多个模块合并在一个文件中。

# AMD模块的写法

requireJS 加载的模块采用 AMD 规范，也就是模块必须按照 AMD 的规范来写，模块必须采用特定的 define() 函数来定义。

## 不依赖其他模块

如果一个模块不依赖其他模块，那么就可以直接定义在 define() 函数中了。比如 math.js

```js
define(function(){
    function sum(a, b){
        return a+b;
    }
    return {
        sum: sum
    };
});
```

## 依赖其他模块

如果这个模块依赖于其他模块，比如：animate.js
【Q.那此处的模块名，也是直接在main里定义的那些吗？还是在各自的js里再次 require.config() 会覆盖么？try下~】

```js
define(['jquery'], function($){
    function setPosition(selector, left, top){
        $(selector).css({
            'position': 'absolute',
            'left': left,
            'top': top
        });
    }
    return {
        setPosition: setPosition
    };
});
```

##jQuery
jQuery 从1.7后开始支持 AMD 规范，即如果jQuery作为一个 AMD 模块运行时，它的模块名是”jquery”，注意”jquery”是固定的。

jQuery 中支持 AMD 的代码如下：

```js
if( typeof define === 'function' && define.amd && define.amd.jQuery ){
    define( "jquery", [], function(){
        return jQuery;
    } );
}
```

jQuery 最终向外暴露的是全局的 jQuery 和 $，即 window.jQuery = window.$ = jQuery
如果将 jQuery 应用在模块化开发时，其实可以不用全局的，即可以不暴露出来。需要用到 jQuery 时使用 require() 函数即可。

# 加载非规范的模块
理论上，requireJS 加载的模块必须是按照 AMD规范、用 define() 定义的模块。但是实际上，requireJS 也能够加载非规范的模块。这样的模块们，在用 require() 加载之前，要先用 require.config() 定义它们的一些特性。 shim 属性专门用来配置不兼容的模块。举例，underscore 和 backbone 这两个库，都没有采用 AMD 规范编写。如果要用 requireJS 加载它们的话，就必须先定义它们的特征。

```js
require.config(
    // shim 属性专门用来配置不兼容的模块
    shim: {
        'underscore': {
            exports: '_'   // 输出的变量名，表明这个模块外部调用时的名称
        },
        'backbone': {
            deps: ['underscore', 'jquery'], // 该模块的依赖性
            exports: 'backbone'
        }
    }
);
```

jQuery插件可以这样定义

```js
require.config(
    shim: {
        'jquery.scroll': {
            deps: ['jquery'],
            exports: 'jQuery.fn.scroll'
        }
    }
);
```

# requireJS 插件

requireJS 还提供了一系列插件，实现特定的功能。比如：
domready 插件（回调函数在页面 DOM 结构加载完成后再运行）、
text 和 image 插件（允许 requireJS 加载文本和图片文件）、
json 和 mdown（用来加载 json 文件和 markdown 文件）等等。


# 参考

RequireJS 入门（一二）
[http://www.cnblogs.com/snandy/archive/2012/05/22/2513652.html](http://www.cnblogs.com/snandy/archive/2012/05/22/2513652.html)
[http://www.cnblogs.com/snandy/archive/2012/05/23/2513712.html](http://www.cnblogs.com/snandy/archive/2012/05/23/2513712.html)

Javascript模块化编程（三）：require.js的用法
[http://www.ruanyifeng.com/blog/2012/11/require_js.html](http://www.ruanyifeng.com/blog/2012/11/require_js.html)
