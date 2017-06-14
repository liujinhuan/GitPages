---
title: MongoDB的增删改查
date: 2017-04-24 17:15:17
tags: 
	- MongoDB
	- Mac
---
> 好像最近没那多鸡汤~直接开始吧~

### 连接
+ 前面一节我们安装了ManogoDB，如果你成功安装了的话～那么，新开终端，输入下述指令进行连接。

```js
mongo
```

+ 出现下述所示，很好，你成功啦～可以以命令行的方式操作啦

```js
MongoDB shell version: 3.2.8
connecting to: test
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
http://docs.mongodb.org/
Questions? Try the support group
http://groups.google.com/group/mongodb-user
Server has startup warnings:
2016-08-02T19:16:07.239+0800 I CONTROL  [initandlisten]
2016-08-02T19:16:07.239+0800 I CONTROL  [initandlisten] ** WARNING: soft rlimits too low. Number of files is 256, should be at least 1000
>
>
>
```

<!-- more -->

+ 如果你没有成功安装mongodb，你可能会出现如下的错误哦～

```js
MongoDB shell version: 3.2.8
connecting to: test
2016-08-02T18:14:33.677+0800 W NETWORK  [thread1] Failed to connect to 127.0.0.1:27017, reason: errno:61 Connection refused
2016-08-02T18:14:33.678+0800 E QUERY    [thread1] Error: couldn't connect to server 127.0.0.1:27017, connection attempt failed :
connect@src/mongo/shell/mongo.js:229:14
@(connect):1:6

exception: connect failed
```

+ 所以，失败的～参考上一节～在安装下～


### 增删改查
1.数据库
+ 查询已有的数据库

```js
show dbs
```

+ 初次安装的话，会出现如下所示的一种数据库

```js
local  0.000GB
```

+ 安装数据库

```js
use 数据库名（如：test）
```

+ 有同名数据库就切换到已有的，没有的话就会创建新的

```js
switched to db test
```

2.集合
+ 创建集合

```js
db.createCollection("集合名字：如（mycollection）")
```

+ 结果

```js
{ "ok" : 1 }
```

+ 查看集合

```js
show collections
```

+ 结果

```js
mycollection（创建的集合名字）
```

3.增：
+ insert（以集合mycollection为例）

```js
db.mycollection.insert({name:"liuqiqi"})
```

+ 结果

```js
WriteResult({ "nInserted" : 1 })
```

4.查：
+ find（以集合mycollection为例）

```js
db.mycollection.find().pretty()
```

+ 结果

```js
{ "_id" : ObjectId("57a0871725ae4f21a42b44e3"), "name" : "liuqiqi" }
```

5.改：
+ update（以集合mycollection为例）。修改name是liuqiqi的为TTTTTT

```js
db.mycollection.update({'name':'liuqiqi'},{$set:{'name':'TTTTTT'}})
```

+ 结果

```js
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```

6.删：
+ remove（以集合mycollection为例）

```js
db.mycollection.remove({"name":"liuqiqi"})
```

+ 结果

```js
WriteResult({ "nRemoved" : 1 })
```

### 可视化操作工具

+ 上述操作都是在终端中输入指令执行的～推荐一款可视化操作工具[Robomongo](https://robomongo.org/)～




