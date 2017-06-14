---
title: XSS攻击学习笔记
date: 2017-04-27 18:15:54
tags: 
    - XSS
    - Node
    - Express
    - ejs
    - web安全
---

> 最近的一次面试题中，有问到XSSE和CSRF。表示当时只知道学名，是“攻击”的意思。。。后来在慕课网中看到一位老师的视频，觉得还不错，就动手跟着学习起来。整理的学习笔记如下。项目源码会在后面贴出，请叫我雷锋~~

### XSS的攻击方式

+ 反射型

> 发出请求是,XSS代码出现在URL中,作为输入提交到服务器端,服务器端解析后响应,XSS代码随着响应内容一起传回浏览器,最后浏览器解析执行XSS代码。这个过程像一次反射,故叫做反射型XSS。

+ 存储型

> 存储型XSS和反射型XSS的差别在于,提交的代码会存储在服务器中(例如数据库,内存,文件系统等),下次请求页面是不用再提交XSS代码。

### XSS的防御

<!-- more -->

+ 编码：对传递的数据进行编码转义，该操作可以在后端或者前端处理

```
“	---->   &quot; 
&	---->   &amp;
<	---->   &lt;
>	---->   &gt;
不间断的空格	---->   &nbsp;
```

+ 过滤：移除掉数据中不合法的元素，标签，属性等

> 移除用户上传到dom属性。如img的onerror属性，可以出发xss攻击。
移除用户上传的style，iframe，script节点


+ 校正

(1)避免直接对html entity解码
> 在 HTML 中，某些字符是预留的。在 HTML 中不能使用小于号（<）和大于号（>），这是因为浏览器会误认为它们是标签。如果希望正确地显示预留字符，我们必须在 HTML 源代码中使用字符实体（character entities）。HTML 中的常用字符实体是不间断空格(&nbsp;)。

(2)使用dom parse转换，校正不匹配的标签
> 对匹配到的标签，属性等进行过滤

(3)示例代码
```js
// 解码
HTMLParser(he.unescape(s,{strict:true}),{
	start:function(tag,attrs,unary){
        // 过滤不合法的标签
        if(tag=='script'||tag=='style'||tag=='link'||tag=='iframe'||tag=='frame')return;
        results += '<'+tag;
        // 这里过滤掉全部的属性，实际中可根据需要有选择性的替换
        // for(var i=0,len=attrs.length;i<len;i++){
        //     results += " "+attrs[i].name+'="'+attrs[i].escaped+'"';
        // }
        results += (unary?"/":"")+">";
    },
    end:function(tag){
        results += "</"+tag+">";
    },
    chars:function(text){
        results += text;
    },
    comment:function(text){
        results +="<!--"+text+"-->";
    }
});
```
### XSS项目实战

[项目源码,叫我雷锋](https://github.com/liujinhuan/XSS.git)
[Web安全-XSS](http://www.imooc.com/learn/812)






