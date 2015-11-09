layout: post
title: 移动端框架初探
date: 2013-06-18
category: 技术
tags: 
description: 简单的说明一下目前的移动端框架, 仅作为个人了解.
---

最近将会展开移动端的项目，在此之前会先评估一下目前市面上比较火的几个移动端框架。就我本人所知道的也仅仅是以下两个：（摔啊！！这么多框架你怎么才知道这两个。。。= =!）

<!-- more -->

> bootstrap
> Fundation
> BluePrint
> Skeleton

## 框架太多
这里只是依据个人理解，简单的阐述一下这几种框架在自己的项目中的优点和缺点（其实也不能算是缺点，应该说在我们的项目里，哪个框架更符合我们的需求）

### bootstrap
`bootstrap`毫无疑问是个优秀的前端框架。
她具有良好的响应式设计和卓越的兼容性，用户在各终端平台（PC、Phone、Pad）下都具备良好的浏览体验。
主要是界面UI**风格统一**，所以你会发现，凡事用此框架开发的站点，其界面必定是有很雷同的地方。
用[LESS][1]进行预编译，最直接的表现是她在[github][2]上fork人数最多，最活跃。各种优点咱就不再赘述了~


### foundation
[Foundation][3]是什么呢？我也是最近才听说过：

>[ZURB][4] 是家擁有 14 年網站設計經驗的公司，他們的前端開發框架「Foundation」是一個開放原始碼專案，
>提供現代網站開發所需的 Prototyping、Grid System、Responsive Design，對平板與智慧型手機的小尺寸螢幕，有很棒的支援。
>ZURB 使用 [SASS][5] 設計網站布局的 CSS3 樣式，因此網頁視覺設計師可以很容易進行外觀的客製。
`by`[玩物喪誌][6]

貌似最新的版本是`foundation4`，目前還沒有用過，打算找個時間看一下其代碼，她的CSS是用SASS進行預編譯的，這點讓我增加了對她的好感度:)

### 這兩個框架用到我們的項目上會有什麼問題？

bootstrap不得不說的一點是其UI已經高度同致化，而我們的項目是有自己的設計風格，若要完全按照bootstrap的來，顯然不行；若要重新寫UI，那麼就要進行深度的二次開發，況且我們的系統相對來說還蠻寵大。

**Foundation最大的特點是支援zepot.js與jquery的轉換。之前我們的項目用的zepot.js，那麼這套框架是很容易支持原來就已有的方法，這在一定呈度上能節約不少開發時間。**


不過，具體選哪個。。待定吧。。



[1]: http://www.lesscss.net/ "LESS中国官网"
[2]: https://github.com/twitter/bootstrap
[3]: http://foundation.zurb.com/ "The most advanced responsive front-end framework in the world."
[4]: http://zurb.com/ "ZURB, creating unique customer and user experiences."
[5]: http://sass-lang.com/
[6]: http://blog.lyhdev.com/2013/01/foundation-3-reponsive.html
