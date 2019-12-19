---
title: 基于Vue+iView+Koa+Mongodb的后台管理系统--客户端
date: 2017-5-16 22:17:12
tags: 
	- Vue
	- iView
	- Koa
	- Mongodb
	- vue-router
	- koa-router
	- vue-resource
---
> 经过6天的奋战，一个后台管理系统已经新鲜出炉了。感觉主要是闲的蛋疼。没事瞎搞。哈哈。

记得在[上一篇博客](https://liujinhuan.github.io/2017/05/01/MongoDB%E7%9A%84%E5%AE%9E%E6%88%98/#more)的尾巴中，承诺大家要做一个前后台通杀的小系统，以在实际的项目中运用。话不多说~开始吧。

### 前言

> 项目来源于大学的毕业设计，仅在实现CURD功能。其中，个别例子存在不合理之处(如：用户密码明文展示在表格中等)，请自行忽略，不要较真儿哦~

### 项目及技术介绍

> 该管理系统主要包括登录、图书管理、用户管理三个部分。可以实现图书与用户的CURD操作。其中admin用户属于管理员，可以操作用户管理，而其余用户则只能操作图书管理。具体的角色权限关系还未考虑在其中，感兴趣的同学，可以自行添加。

<!-- more -->

+ client

整体采用Vue框架。通过`vue-cli`脚手架工具生成前端基本项目目录，通过`vue-router`组件实现单页面路由，通过`vue-resource`实现数据请求的发送，通过`iView`前端UI框架实现页面的展示。

+ server

整体采用Koa框架。通过`generator-koa2-rest`脚手架工具生成后端基本项目目录，通过`mongoose`中间件完成和数据库的链接，通过`koa-router`中间件实现接口的路由，通过`koa-bodyparser`中间件获取用户的请求参数，通过`koa-cors`中间件解决跨域请求。


### Client搭建

+ 全局安装 vue-cli

```javascript
npm install --global vue-cli
```

+ 创建一个基于 webpack 模板的新项目

```javascript
vue init webpack client(目录名称)
```
![基于 webpack 模板的新项目](https://raw.githubusercontent.com/liujinhuan/LearnNotes/master/imgs/AdminBook/client/1.png)

+ 安装依赖及运行

```javascript
cd client && npm install && npm run dev
```

+ 安装iView

```javascript
npm install iview --save
```
![安装iView](https://raw.githubusercontent.com/liujinhuan/LearnNotes/master/imgs/AdminBook/client/2.png)


+ 在 webpack 入口页面 main.js 中配置iView：

```javascript
import iView from 'iview'
import 'iview/dist/styles/iview.css'   // 使用 CSS

Vue.use(iView);			//引用iView组件
```

+ 具体使用可参照[iView官网API](https://www.iviewui.com/)在vue文件中进行引用和操作等。

+ 引入vue-resource和vue-router组件
```javascript
import VueResource from 'vue-resource'
Vue.use(VueResource)

import Router from 'vue-router'
Vue.use(Router)
```

### 过程记录

+ 各技术栈的官网还是要提前看一下，不然撸起代码都不顺畅。

+ 路由：创建完模块页面之后，在router/index.js中记得导入和配置路由。
+ 子路由：后期的路由部分做了比较大的调整，主要为了解决引入菜单栏后，目标页面无法显示在内容区的问题。

```javascript
export default new Router({
  mode: 'history', // 指定路由采用history方式
  routes: [
    {
      path: '/home',
      name: 'home',
      component: Home,
      children: [ //如下路由均为home的子路由,使其可以显示在home的路由之下
        {
          path: '/',
          name: 'home',
          component: BookList
        },
        {
          path: '/booklist',
          name: 'booklist',
          component: BookList
        },
        。。。。。。// 省略号
        { 
          path: '/userdetail', 
          name: 'userdetail',
          component: UserDetail
        }
      ]
    },
    {
      path: '/',
      name: 'login',
      component: Login
    }

  ]
})
```
+ 请求的发送：采用引入`vue-resource`来触发http请求。如：

```javascript
this.$http.post/get(Url地址,入参).then(response => {
    response	// 成功接口返回值
}, response => {
    response	// 失败接口返回值
});
```

+ 页面跳转：采用`vue-router`进行单页面路由

```javascript
this.$router.go(-1);    // 后退页面
this.$router.push({ name: 'bookdetail' , query: { bookid: this.data[index]._id }});		// 参数在url的页面跳转
this.$router.push({ name: 'bookupdate', params: { book:updateBook }});	// 参数在body中的页面跳转
this.$router.push({name:'bookadd'});	// 不带参数的跳转
```

+ 工具类：该项目有store本地存储和url请求地址两个工具类，引用时注意路径。后在`webpack.base.conf.js`中发现`@`路径代表的就是当前根目录`src`，所以可直接如下方式引用

```javascript
import Store from '@/utils/store'
import Url from '@/utils/url'
```

### 项目截图
+ 登录
![Login](https://raw.githubusercontent.com/liujinhuan/LearnNotes/master/imgs/AdminBook/client/login.png)
+ home主页
![home](https://raw.githubusercontent.com/liujinhuan/LearnNotes/master/imgs/AdminBook/client/home.png)
+ 图书列表的请求
![booklist](https://raw.githubusercontent.com/liujinhuan/LearnNotes/master/imgs/AdminBook/client/booklist.png)
+ 图书的添加
![bookadd](https://raw.githubusercontent.com/liujinhuan/LearnNotes/master/imgs/AdminBook/client/bookadd.png)
+ 图书的修改
![bookupdate](https://raw.githubusercontent.com/liujinhuan/LearnNotes/master/imgs/AdminBook/client/bookupdate.png)
+ 图书的详情
![bookdetail](https://raw.githubusercontent.com/liujinhuan/LearnNotes/master/imgs/AdminBook/client/bookdetail.png)
+ 图书的删除
![bookdelete](https://raw.githubusercontent.com/liujinhuan/LearnNotes/master/imgs/AdminBook/client/bookdelete.png)


> 有种喜悦叫做从无到有。Server端的博客后续推出~敬请期待。