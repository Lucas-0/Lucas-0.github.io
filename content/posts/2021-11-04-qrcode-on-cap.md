---
title: "关于我和瓶盖斗智斗勇这件事"
subtitle: ""
date: 2021-11-04T23:10:26+08:00
weight: 
lastmod: 
draft: 
author: "Lucas"
authorLink: "https://github.com/Lucas-0"
description: ""
summary: ""
license: ""
# 移动端网页链接的图片
images: []
# 过期时间 超过这个时间文章不会出现网站上
expiryDate: 
# 发布时间可在未来
publishDate: 

tags: []
categories: ["生活"]
# 文章顶部照片
featuredImage: ""
# 文章在首页的缩略图 550*164px
featuredImagePreview: "https://raw.githubusercontent.com/Lucas-0/IMG/master/img/202111051714703.jpg"

hiddenFromHomePage: false
hiddenFromSearch: false
twemoji: false
lightgallery: true
ruby: true
fraction: true
fontawesome: true
linkToMarkdown: false
rssFullText: false

toc:
  enable: false
  auto: true
code:
  copy: true
  # ...
math:
  enable: true
  # ...
mapbox:
  accessToken: ""
  # ...
share:
  enable: true
  # ...
comment:
  enable: true
  # ...
library:
  css:
    # someCSS = "some.css"
    # 位于 "assets/"
    # 或者
    # someCSS = "https://cdn.example.com/some.css"
  js:
    # someJS = "some.js"
    # 位于 "assets/"
    # 或者
    # someJS = "https://cdn.example.com/some.js"
seo:
  images: []
  # ...
---
时至今日，饮料商家促销已经放弃了传统的再来一瓶方案。在笔者的体验中，这一方案最大的缺点是商家（主要是城乡结合部的小卖部）未必承认和配合，原因易见：对他们来说，这活动对他们没有益处，收集的瓶盖还要拿去上一级兑换，徒费功夫。目前饮料促销大都选择了瓶身二维码的形式。但是在瓶盖的小小空间中，二维码的辨识度并不太好。本文即记录了笔者与之斗争的过程。
<!--more-->

{{< image src="https://raw.githubusercontent.com/Lucas-0/IMG/master/img/202111042311591.png" caption="Bottle Cap">}}
如图，瓶盖上的二维码采用点阵的形式。由于和背景的对比度低，导致无论是微信还是系统自带相机都无法识别到。尝试使用更大的放大倍数，但是瓶盖上的瑕疵甚至比二维码放大得更多，对比度反而下降了。另外尝试调整瓶盖对光角度使得反射光正对镜头，画面中二维码亮度虽有增加但是仍以无效告终。

这时笔者想到，可以结合以上两种方法，并且在瓶盖上倒一些水以掩盖放大后的背景瑕疵<!--什么深紫外光刻-->。果然，此法下背景保持不变，二维码更加清晰，可惜依旧识别不能。

貌似万策尽。走投无路，此时的笔者决定开启假设性原则。想到，一切措施都是假设对比度不够导致识别失败的情况下做出的，那么我们还有什么可利用的呢？没错，点阵和背景的反射率不同。笔者使用手电照亮瓶盖，此时的二维码闪着诡异的光，识别成功。

Q.E.D.