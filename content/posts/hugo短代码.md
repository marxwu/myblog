---
title: "Hugo短代码"
date: 2022-12-07T11:52:17+08:00
draft: false

featured_image: "images/hugoshortcode.png"
tags: ["hugo", "shortcode"]
categories: "hugo"
---


第一种写法：
```
hello color="red"

<p>
    <h1 style="color: {{ .Get `color` }} ">
        Hello World! 
    </h1>
</p>
```
  
第二种写法：
```
hello red

<p>
    <h1 style="color: {{ .Get 0 }} ">
        Hello World! 
    </h1>
</p>
```
