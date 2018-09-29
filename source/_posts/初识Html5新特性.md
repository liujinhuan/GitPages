---
title: 初识Html5新特性
date: 2017-6-14 21:22:51
tags: 
    - html
    - html5
---

> 偶然的情况下，会被问及平时用过哪些Html5新特性呀？懵逼。顿时懵逼。通过查看文档，了解到，其实我们项目中还是有很多地方用到了新特性。今天我们来一起总结下。

### 概述

+ HTML5 是下一代的 HTML。HTML5 是 W3C 与 WHATWG 合作的结果。
+ 新特性

> 用于绘画的 canvas 元素
用于媒介回放的 video 和 audio 元素
对本地离线存储的更好的支持
新的特殊内容元素，比如 article、footer、header、nav、section
新的表单控件，比如 calendar、date、time、email、url、search

<!-- more -->

+ 浏览器支持

> 最新版本的 Safari、Chrome、Firefox 以及 Opera 支持某些 HTML5 特性。Internet Explorer 9 将支持某些 HTML5 特性。

### 新特性

| 新特性      | 标签   |   Description		|
| ------------- |:-------------:|-------------:|
|视频|video|用于视频播放，提供视频播放标准，html新标签|
|音频|audio|用于音频播放，提供音频播放标准，html新标签|
|画布|canvas|使用Javacript在网页上绘制图像，html新标签|
|可伸缩矢量图形|SVG|使用xml定义网络基于矢量的图形，html新标签|
|地理定位|Geolocation|用于获得用户的地理位置|
|web存储|localStorage|永久性存储|
|web存储|sessionStorage|会话性存储|
|应用程序缓存|cache manifest 文件|使应用进行缓存，并在没有网络的情况下访问。文件三个部分：CACHE MANIFEST，NETWORK，FALLBACK|
|运行在后台的 JavaScript|Worker|运行在后台的独立脚本，通过postMessage/onmessage来回传和监听消息|
|服务器发送事件|EventSource|网页自动获取来自服务器的更新|

### 新增Input类型
| 新Input类型      | 取值   |   Description		|
| ------------- |:-------------:|-------------:|
| e-mail地址|type="email"|在提交表单时，会自动验证 email 域的值|
|URL 地址 |type="url"|在提交表单时，会自动验证 url 域的值|
|数值|type="number"|可设定所接受的数字范围min和max|
|一定范围的数字| type="range"|显示为滑动条,可以设定对所接受的数字的限定min和max|
|日期选择器|type="date"|选取日、月、年|
|日期选择器|type="month"|选取月、年|
|日期选择器|type="week"|选取周、年|
|日期选择器|type="time"|选取时间（小时和分钟）|
|日期选择器|type="datetime"|选取时间、日、月、年（UTC 时间）|
|日期选择器|type="datetime-local"|选取时间、日、月、年（本地时间）|
|搜索域|type="search"|显示为常规的文本域|

### 表单元素
| 表单元素      | 取值   |   Description		|
| ------------- |:-------------:|-------------:|
|输入域选项表|datalist|通过input标签的list属性指向datalist所在id，即可把 datalist 绑定到输入域|
|验证用户|keygen|密钥对生成器|
|不同类型输出|output|比如：计算或脚本输出|

### 表单属性
| 表单属性     |    描述		|取值|
| ------------- :|-------------:|-------------:|
|autocomplete|自动补全功能|on/off|
|novalidate|提交表单时不应该验证 form 或 input 域|true/false|

### input 属性
| input属性     |    描述		|取值|
| ------------- :|-------------:|-------------:|
|autocomplete|自动补全功能|on/off|
|autofocus|页面加载时域自动地获得焦点|autofocus|
|form|输入域所属的一个或多个表单|所属表单的id|
|height| image 类型的 input 标签的图像高度|数值|
|width| image 类型的 input 标签的图像宽度|数值|
|list|输入域的 datalist，datalist 是输入域的选项列表|datalist的id|
|min|输入域所允许的最小值|数值|
|max|输入域所允许的最大值|数值|
|step|输入域规定合法的数字间隔|数值|
|multiple|输入域中可选择多个值，适用于email 和 file|multiple|
|pattern|用于验证 input 域的模式，适用于text, search, url, telephone, email 以及 password|正则表达式|
|placeholder|提示（hint），描述输入域所期待的值，适用于text, search, url, telephone, email 以及 password||
|required|必填|required|


> 我谦好帅~