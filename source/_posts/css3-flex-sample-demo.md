title: css3-flex-sample-demo
date: 2014-12-11 09:17:38
categories: flex
tags: css3
description: 是时候把flex这个属性好好的研究一下了。
---
>我写的东西总感觉是干瘪的很。。我尽量写的丰富多彩些。不过总体上不影响理解的哈哈哈.
>css兼容性前缀用后处理器来解决。autoprefixer

直接进入正题了，不说废话。

## 1

`div.flex-box>(div.flex-items)*3`这个html结构，很简单。
两个div，一个父级`.flex-box`，三个子元素`.flex-items`。

给`.flex-box`元素设置`display`属性为`flex`或`inline-flex`即可把`.flex-box`设置为伸缩容器。

给`.flex-item`元素设置`box-flex:1`则表示这个元素所占的宽度，而且是流体。

以上，是不是非常简单啊。其实常用到的也差不多是这个样子了。无非还有一些以下的功能。
<!-- more -->

## 2
如果三个子元素需要**两端对齐**且平均分布在`.flex-box`内，则需要对`.flex-box`设置`justify-content`的属性为`space-between`。

`justify-content`主轴方向内容对齐方式

>flex-srart（默认）：与主轴起始方向对齐。
>flex-end：向主轴终点方向对齐。
>center：向主轴中点方向对齐。
>space-between：起始位置向主轴起始方向对齐，终点位置向主轴终点方向对齐，其余位置向主轴中点方向对齐。
>space-around：与space-between类似，只是起始位置和终点位置保留一半空白。

用一些喜闻乐见的图片来解释上面的值。
![justify-content]({{BASE_PATH}}/img/css3-flex-sample-demo/justify-content.png)

## sample demo

![smaple-demo]({{BASE_PATH}}/img/css3-flex-sample-demo/sample-demo.jpg)

#### 代码
html
```html
<div class="bdsharebuttonbox " data-tag="jia-share" data-bd-bind="">
    <a class="bds_weixin" data-cmd="weixin" href="#" title="分享到微信"></a>
    <a class="bds_tsina " data-cmd="tsina" title="分享到新浪微博"></a>
    <a class="bds_qzone" data-cmd="qzone" title="分享到QQ空间"></a>
    <a class="bds_tqq" data-cmd="tqq" title="分享到腾讯微博"></a>
    <a class="bds_qq" data-cmd="qq" title="分享到QQ收藏"></a>
    <a class="bds_renren " data-cmd="renren" title="分享到人人网"></a>
</div>
```
css
```css
.bdsharebuttonbox {
    background: #fff;
    padding: 10px 0;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
    -webkit-justify-content: space-between;
    -ms-flex-pack: justify;
    justify-content: space-between;
}

.bdsharebuttonbox a {
    background-repeat: no-repeat;
    cursor: pointer;
    margin: 6px 6px 6px 0;
    overflow: hidden;
    color: #3a8ceb;
    width: 90px;
    height: 90px;
    -webkit-box-flex: 1;
    -moz-box-flex: 1;
    box-flex: 1;
    -webkit-box-direction: normal;
}

```


codepen
<p data-height="268" data-theme-id="4818" data-slug-hash="vEGOGj" data-default-tab="result" data-user="jcpplus" class='codepen'>See the Pen <a href='http://codepen.io/jcpplus/pen/vEGOGj/'>css3-flex-sample-demo</a> by jcpplus (<a href='http://codepen.io/jcpplus'>@jcpplus</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>



