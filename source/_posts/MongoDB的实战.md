---
title: Node下MongoDB的实战
date: 2017-05-01 22:52
tags: 
	- MongoDB
	- Node
	- Mac
---

> 在听陈鸿宇的《理想三旬》。好听～

上两篇博文中提到了在Mac下MongoDB的安装与连接，这次我们来看看如何在Node命令行的形式下，操MongoDB
PS：本文中的数据集合采用上篇博文中“test”库中的“mycollection”。

### 安装MongoDB包

+ 使用Node中的mongodb模块，需要先安装哦～打开终端，输入如下命令～

```js
npm install mongodb
```

### 数据库的链接与断开

<!-- more -->

+ 引入mongodb模块
```js
var mongo = require("mongodb");
```

+ 创建MongoDB数据库的服务器对象
```js
var server = new mongo.Server(host,port,[options]);
```
> 说明：host：服务器所在地址，默认本地localhost；port：服务器端口号，默认27017；options：可选配置参数。

+ 创建MongoDB的db对象
```js
var db = new mongo.Db(databasename,server,[options]);
```
> 说明：databasename：数据库名，这里我们使用上篇的“test”数据库；server：服务器对象；options：可选配置参数。

+ 执行db的open方法，连接数据库
```js
db.open(callback(err,db));
```
> 说明：callback回调方法，如果连接失败，将抛出err错误，连接数据库成功，会返回db对象。

+ 执行db的close方法，断开数据库连接
```js
db.close();
```
> 说明：关闭数据库连接时，将会触发监听的close事件，该事件有err和db两参数，意义同上。

```js
function(err,db){
    //回调方法
}
```
+ 附：代码片段。将下述代码保存在testMongo.js文件中。

```js
var mongo = require("mongodb");
var host = "localhost";
var port = "27017";

var server = new mongo.Server(host,port,{auto_reconnect:true});

var db = new mongo.Db("test",server,{safe:true});

db.open(function(err,db){
	if(err){
		throw err;
		console.log("连接数据库出错");
	}else{
		console.log("成功建立数据库连接");
		db.close();
	}
});

db.on("close",function(err,db){
	if(err){
		throw err;
		console.log("连接数据库出错");
	}else{
		console.log("关闭数据库连接")
	}
})
```

+ 新开终端，输入"mongod"打开mongodb。
+ 新开终端，输入"node testMongo.js"，看到如下结果，就成功啦。
```js
testNode  node testMongo.js
成功建立数据库连接
关闭数据库连接
```

### 数据集合

+ MongoDb操作的是数据集合！！！数据的操作就是对数据集合的操作。
```js
db.collection(collectionname,[options],callback(err,collection));
```
> 说明：collectionname：数据库中数据集合名字，此处是上节的"mycollection"；options：可选配置参数。callback：连接的回调方法，会有连接出错的err参数和连接成功的collecction参数。

+ 附：代码片段。保存下述文件到testMongo.js中相应位置。
```js
console.log("成功建立数据库连接");
<!-- 数据集合 -->
db.collection('mycollection',function(err,collection){
	if(err){
		throw err;
		console.log("连接数据集合出错");
	}else{
		console.log("成功连接数据集合");
		db.close();
	}
});
<!-- 数据集合 -->
```

+ 新开终端，输入"node testMongo.js"，看到如下结果，就成功啦。

```js
testNode  node testMongo.js
成功建立数据库连接
成功连接数据集合
关闭数据库连接
```

### MongoDb－增
+ 数据集合的insert方法，实现添加数据的操作。
```
collection.insert(docs,[options],[callback(err,docs)])
```

> 说明：docs：要插入的数据；options：可选配置参数。可选callback：插入的回调方法，插入出错的err参数和插入成功时的docs（插入的数据）参数。

+ 附：代码片段。保存下述文件到testMongo.js中相应位置。－－在test库的mycollection数据集合中插入5条Cailala

```js
console.log("成功连接数据集合");
<!-- insert start-->
for(var i = 1;i<6;i++){
	collection.insert({'name':'Cailala'+i},function(err,docs){
		console.log(docs);
		db.close();
	});
}
<!-- insert end-->
```
+ 新开终端，输入"node testMongo.js"，看到如下结果，就成功啦。

```js
testNode  node testMongo.js
成功建立数据库连接
成功连接数据集合
{ result: { ok: 1, n: 1 },
  ops: [ { name: 'Cailala1', _id: 57a1fb5292764dbc5736dcd9 } ],
  insertedCount: 1,
  insertedIds: [ 57a1fb5292764dbc5736dcd9 ] }
关闭数据库连接
{ result: { ok: 1, n: 1 },
  ops: [ { name: 'Cailala2', _id: 57a1fb5292764dbc5736dcda } ],
  insertedCount: 1,
  insertedIds: [ 57a1fb5292764dbc5736dcda ] }
{ result: { ok: 1, n: 1 },
  ops: [ { name: 'Cailala3', _id: 57a1fb5292764dbc5736dcdb } ],
  insertedCount: 1,
  insertedIds: [ 57a1fb5292764dbc5736dcdb ] }
{ result: { ok: 1, n: 1 },
  ops: [ { name: 'Cailala4', _id: 57a1fb5292764dbc5736dcdc } ],
  insertedCount: 1,
  insertedIds: [ 57a1fb5292764dbc5736dcdc ] }
{ result: { ok: 1, n: 1 },
  ops: [ { name: 'Cailala5', _id: 57a1fb5292764dbc5736dcdd } ],
  insertedCount: 1,
  insertedIds: [ 57a1fb5292764dbc5736dcdd ] }
```

### MongoDb－查
+ 数据集合的find方法，实现查询数据的操作。
```js
collection.find(selector,[options]).toArray(callback(err,docs))
```
> 说明：selector：查询条件；options：可选配置参数。find方法返回的是Cursor游标对象，该对象的toArray方法将返回查询到的所有数据文档，参数callback：查询的回调方法，查询出错的err参数和查询成功时的docs（查询出的数据）参数。

+ 附：代码片段。保存下述文件到testMongo.js中相应位置。－－查询数据集合中name是Cailala1的数据

```js
console.log("成功连接数据集合");
<!-- find -->
collection.find({name:"Cailala1"},{fields:{name:1,_id:0}}).toArray(function(err,docs){
	if(err) throw err;
	else 
		console.log(docs);
		db.close();
});
<!-- find -->
```
+ 新开终端，输入"node testMongo.js"，看到如下结果，就成功啦。
```js
testNode  node testMongo.js
成功建立数据库连接
成功连接数据集合
[ { name: 'Cailala1' } ]
关闭数据库连接
```

### MongoDb－改
+ 数据集合的update方法，实现修改数据的操作。
```js
collection.update(selector,documents,[optios],[callback(err,resu)])
```
> 说明：selector：需要更新的数据文档；documents：用于更新的文档；options：可选配置参数；可选callback：修改的回调方法，修改出错的err参数和修改成功时的result（成功修改的数据条数）参数。

+ 附：代码片段。保存下述文件到testMongo.js中相应位置。－－修改name是Cailala1为liujinhuan，并查询输出。

```js
console.log("成功连接数据集合");
<!-- update -->
collection.update({name:"Cailala1"},{name:"liujinhuan"},function(err,res){
	if(err){
		throw err;
	}else{
		console.log("成功更新 "+JSON.parse(res).n+"  条数据");
		collection.find({},{fields:{name:1,_id:0}}).toArray(function(err,docs){
				if(err) 
					throw err;
				else 
					console.log(docs);
					db.close();
		});
	}
});
<!-- update -->
```
+ 新开终端，输入"node testMongo.js"，看到如下结果，就成功啦。
```
testNode  node testMongo.js
成功建立数据库连接
成功连接数据集合
成功更新 1  条数据
[ { name: 'liujinhuan' },
  { name: 'Cailala2' },
  { name: 'Cailala3' },
  { name: 'Cailala4' },
  { name: 'Cailala5' } ]
关闭数据库连接
```

### MongoDb－删
+ 数据集合的remove方法，实现删除数据的操作。
```js
collection.remove([selector],[options],[callback])
```

> 说明：可选selector：删除的条件，不指定则删除全部；可选options：配置参数；可选callback：删除的回调方法，删除出错的err参数和删除成功时的result（成功修改的数据条数）参数。

+ 附：代码片段。保存下述文件到testMongo.js中相应位置。

```js
console.log("成功连接数据集合");
<!-- remove -->
collection.remove({name:"liujinhuan"},function(err,res){
	if(err){
		throw err;
	}else{
		console.log("成功删除 "+JSON.parse(res).n+"  条数据");
		collection.find({},{fields:{name:1,_id:0}}).toArray(function(err,docs){
				if(err) 
					throw err;
				else 
					console.log(docs);
					db.close();
		});
	}
});
<!-- remove -->
```

+ 新开终端，输入"node testMongo.js"，看到如下结果，就成功啦。
```js
testNode  node testMongo.js
成功建立数据库连接
成功连接数据集合
成功删除 1  条数据
[ { name: 'Cailala2' },
  { name: 'Cailala3' },
  { name: 'Cailala4' },
  { name: 'Cailala5' } ]
关闭数据库连接
```

> 以上就是命令行下的MongoDB操作。其中的options都是一些可以配置的参数～这里只是基础的用法啦～考虑搞一个前后端的小项目实战下~筹备中。怀挺~

听不懂《理想三旬》。但还是在听～直到听吐为止吧～

