title: 多行文本溢出
date: 2015-06-12
category: 
tags: css
keywords: 文本溢出，文本超出隐藏，文本超出显示...

---

大家应该都知道用`text-overflow:ellipsis`属性来实现单行文本的溢出显示省略号(`…`)。当然部分浏览器还需要加宽度`width`属性。

    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;

但是这个属性并不支持多行文本溢出显示省略号，这里根据应用场景介绍几个方法来实现这样的效果。

# WebKit浏览器或移动端的页面

在WebKit浏览器或移动端（绝大部分是WebKit内核的浏览器）的页面实现比较简单，可以直接使用WebKit的CSS扩展属性(WebKit是私有属性)`-webkit-line-clamp` ；注意：这是一个不规范的属性（[unsupported WebKit property](http://developer.apple.com/safari/library/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-UnsupportedProperties)），它没有出现在 CSS 规范草案中。

`-webkit-line-clamp`用来限制在一个块元素显示的文本的行数。 为了实现该效果，它需要组合其他的WebKit属性。
常见结合属性：

`display: -webkit-box;` 必须结合的属性 ，将对象作为弹性伸缩盒子模型显示 。
`-webkit-box-orient` 必须结合的属性 ，设置或检索伸缩盒对象的子元素的排列方式 。
`text-overflow: ellipsis;`可以用来多行文本的情况下，用省略号“…”隐藏超出范围的文本 。

    overflow : hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;

这个属性比较合适WebKit浏览器或移动端（绝大部分是WebKit内核的）浏览器。

具体例子可以看：[这里](http://www.css88.com/webkit/-webkit-line-clamp/)

# 跨浏览器兼容的方案
比较靠谱简单的做法就是设置相对定位的容器高度，用包含省略号(…)的元素模拟实现；

例如：

    p {
        position:relative;
        line-height:1.4em;
        /* 3 times the line-height to show 3 lines */
        height:4.2em;
        overflow:hidden;
    }
    p::after {
        content:"...";
        font-weight:bold;
        position:absolute;
        bottom:0;
        right:0;
        padding:0 20px 1px 45px;
        background:url(http://css88.b0.upaiyun.com/css88/2014/09/ellipsis_bg.png) repeat-y;
    }

这里注意几点：

- height高度真好是`line-height`的3倍；
- 结束的省略好用了半透明的png做了减淡的效果，或者设置背景颜色；
- IE6-7不显示content内容，所以要兼容IE6-7可以是在内容中加入一个标签，比如用`<span class="line-clamp">...</span>`去模拟；
- 要支持IE8，需要将`::after`替换成`:after`；

# JavaScript 方案
用js也可以根据上面的思路去模拟，实现也很简单，推荐几个做类似工作的成熟小工具：

1: [jQuery.dotdotdot](https://github.com/BeSite/jQuery.dotdotdot)

像下面这样用

    $(document).ready(function() {
        $("#wrapper").dotdotdot({
            //  configuration goes here
        });
    });

# 参考

[http://www.cssmojo.com/line-clamp_for_non_webkit-based_browsers/#what-can-we-do-across-browsers](http://www.cssmojo.com/line-clamp_for_non_webkit-based_browsers/#what-can-we-do-across-browsers)
[http://css-tricks.com/line-clampin/](http://css-tricks.com/line-clampin/)
