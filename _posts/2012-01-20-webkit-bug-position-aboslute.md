---
layout: post
title: webkit bug一则：浮动元素下的绝对定位元素
category: 技术总结
tags: [css, 浮动和绝对定位]
excerpt: >
  在做图片上传的图片列表时，图片右上角有一个叉号，用来删除已上传图片。这个小叉号在其他未上传图片的框里是不显示的，因此用到了绝对定位元素的隐藏-显示。但是出现了一个问题：当图片上传完成后，绝对定位的小叉号把图片挤下去了...
---

在做图片上传的图片列表时，图片右上角有一个叉号，用来删除已上传图片。这个小叉号在其他未上传图片的框里是不显示的，因此用到了绝对定位元素的隐藏-显示。但是出现了一个问题：当图片上传完成后，绝对定位的小叉号把图片挤下去了。

按理说绝对定位的元素是脱离文档流的，不应该对文档流中的元素有干扰，可是问题就是出现了。开发时一直用chrome，没想到会是webkit内核的问题。但火狐，IE（甚至是IE6）都没有这个问题。

网上查资料找到点线索，应该是webkit的一个bug，但还不是非常明了。继续查下去，似乎这个问题和浮动元素有关，于是回头看我的html文档结构，果然叉号的父元素是浮动的。于是把叉号挪到不浮动的一个内层div中——问题解决。

看来webkit在渲染页面的时候，遇到浮动元素的绝对定位子元素由隐藏变为显示而出现了混乱。解决方法如前面所说，把这个绝对定位的元素挪到一个非浮动的元素中去就行了。
