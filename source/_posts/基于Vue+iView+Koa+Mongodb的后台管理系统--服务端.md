---
title: 基于Vue+iView+Koa+Mongodb的后台管理系统--服务端
date: 2017-5-17 21:20
tags: 
	- Vue
	- iView
	- Koa
	- Mongodb
	- vue-router
	- koa-router
	- vue-resource
---
> [上一篇博客](https://liujinhuan.github.io/2017/05/16/%E5%9F%BA%E4%BA%8EVue+iView+Koa+Mongodb%E7%9A%84%E5%90%8E%E5%8F%B0%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9F--%E5%AE%A2%E6%88%B7%E7%AB%AF/)中我们主要介绍了客户端的部分，今天来整理下服务端。Go。


### Server搭建

+ 全局安装koa脚手架工具[generator-koa2-rest](https://www.npmjs.com/package/generator-koa2-rest)

```javascript
npm install -g generator-koa2-rest
```

+ 新建目录及初始化

```javascript
mkdir server && cd server && yo koa2-rest 
```

<!-- more -->

+ 安装依赖及运行

```javascript
npm install --save && npm start
```

+ 数据库配置与链接

```
src/config/index.js
----------------------------------------
mongoIp: process.env.IP || 'localhost',
mongoPort: 27017,
mongoDbName: 'management'
```

```
server/index.js
----------------------------------------
const mongoose = require('mongoose');
const db = mongoose.connect("mongodb://"+config.mongoIp+":"+config.mongoPort+"/"+config.mongoDbName);
```

+ koa组件引入
```
import cors from 'koa-cors';//为了解决跨域问题
import parser from 'koa-bodyparser';//框架自动引入的
app.use(cors());
app.use(parser({
  strict: false
}));
```

+ 业务路由创建，脚手架会自动创建model/controller
```
yo koa2-rest:api resource-name(如项目中的book/user/login等，按功能分类)
```

+ 路由配置：创建好的上述路由需在src/index中导出，以供routes配置使用
```
server/src/index.js
----------------------------------------
export root from './root';
export book from './book';
export user from './user';
export login from './login';
```

```
server/config/routes.js
----------------------------------------
'use strict';

import mount from 'koa-mount';
import { root } from '../api';
import { book } from '../api';
import { user } from '../api';
import { login } from '../api';

export default function configRoutes(app) {
  app.use(mount('/', root.routes()));
  // List Endpoints Here
  app.use(mount('/book', book.routes()));// 接口访问的根路由
  app.use(mount('/user', user.routes()));
  app.use(mount('/login', login.routes()));
}
```


### 过程记录

+ 各技术栈的官网还是要提前看一下，不然撸起代码都不顺畅。（这话好像很熟悉的样子。哈哈）

+ npm start报错，可以从以下几点查找原因

| 可能原因 |  解决办法 | 
| ----    | :------------: | 
| node版本是否最新| 开发过程中安装某一个包时要求Node版本是最新。在控台终端可查看原因|
| koa各中间件版本是否匹配| 在安装koa-bodyparser时候需要根据koa的版本进行匹配安装。因为koa的版本是@next，所以最后的安装语句为`npm i koa-bodyparser@next --save`。多加一个@next。在控台终端可查看原因|
| mongodb是否启动 | 若没启动，控制台可见提示错误。需新建终端窗口，启动服务。指令为：`mongod`|

+ 跨域问题

项目的开发调试阶段一直在打开跨域访问的Chrome上进行(之前一直没发现)。后来在Safari上打开了一次，页面数据全没了。通过`console`窗口看到是数据跨域的问题。通过引入`koa-cors`中间件，解决该问题。

```
open -a /Applications/Google\ Chrome.app --args --disable-web-security --user-data-dir=/Users/电脑用户名/workspace/google
```

+ 调试问题

请求的接口没有数据返回？首先可以查看终端server窗口是不是报错，根据提示，找到原因，解决报错。
如果没有报错呢？我目前的方法是通过在可能出错的地方合理使用`console.log`进行调试。

### 项目遗留

+ 项目的部署

据说是要选择一个服务器，然后可以通过pm2等方式进行部署。这个还没开始。有待补充~~


> 一个人，在什么样的情况下，才会知道自己想要的到底是什么呢？




