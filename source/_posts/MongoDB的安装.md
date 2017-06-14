---
title: MongoDB的安装
date: 2017-04-24 16:00:17
tags: 
	- MongoDB
	- Mac
---
> 之前一直在其他平台发布着自己的博客，现在发现GithubPages这个东东~再加上绚丽的主题~~又可以好好的装逼了。那我们撸起袖子，开始干。

### HomeBrew简介与安装
+ 简介：就是mac上的软件包管理工具，方便安装与卸载。
+ 安装：打开终端，输入如下命令，期间会输入一次回车＋两次开机密码。

```js
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### MongoDB安装
+ 打开终端，输入下述指令

```js
brew update
```

+ 继续输入下面指令，期间会出现约两次进度条（忘记截图）

```js
brew install mongodb
```

<!-- more -->

+ 输入指令，启动Mongodb
```js
mongod
```

+ 出现如下报错：约是说没有`/data/db`目录的。

```js
2016-08-02T18:19:16.825+0800 I CONTROL  [initandlisten] MongoDB starting : pid=37113 port=27017 dbpath=/data/db 64-bit host=C02Q6N1GFVH5-3.local
2016-08-02T18:19:16.826+0800 I CONTROL  [initandlisten] db version v3.2.8
2016-08-02T18:19:16.826+0800 I CONTROL  [initandlisten] git version: ed70e33130c977bda0024c125b56d159573dbaf0
2016-08-02T18:19:16.826+0800 I CONTROL  [initandlisten] OpenSSL version: OpenSSL 1.0.2h  3 May 2016
2016-08-02T18:19:16.826+0800 I CONTROL  [initandlisten] allocator: system
2016-08-02T18:19:16.826+0800 I CONTROL  [initandlisten] modules: none
2016-08-02T18:19:16.826+0800 I CONTROL  [initandlisten] build environment:
2016-08-02T18:19:16.826+0800 I CONTROL  [initandlisten]     distarch: x86_64
2016-08-02T18:19:16.826+0800 I CONTROL  [initandlisten]     target_arch: x86_64
2016-08-02T18:19:16.826+0800 I CONTROL  [initandlisten] options: {}
2016-08-02T18:19:16.828+0800 I STORAGE  [initandlisten] exception in initAndListen: 29 Data directory /data/db not found., terminating
2016-08-02T18:19:16.828+0800 I CONTROL  [initandlisten] dbexit:  rc: 100
```

+ 继续输入指令，创建`/data/db`，解决上述问题。期间会出入一次开机密码

```js
sudo chown -R 用户名 /data/db
```

+ 再次试着启动Mongodb

```js
mongod
```
+ waitting 27017。。。成功啦！！！

```js
2016-08-02T19:16:06.621+0800 I CONTROL  [initandlisten] MongoDB starting : pid=38338 port=27017 dbpath=/data/db 64-bit host=C02Q6N1GFVH5-3.local
2016-08-02T19:16:06.622+0800 I CONTROL  [initandlisten] db version v3.2.8
2016-08-02T19:16:06.622+0800 I CONTROL  [initandlisten] git version: ed70e33130c977bda0024c125b56d159573dbaf0
2016-08-02T19:16:06.622+0800 I CONTROL  [initandlisten] OpenSSL version: OpenSSL 1.0.2h  3 May 2016
2016-08-02T19:16:06.622+0800 I CONTROL  [initandlisten] allocator: system
2016-08-02T19:16:06.622+0800 I CONTROL  [initandlisten] modules: none
2016-08-02T19:16:06.622+0800 I CONTROL  [initandlisten] build environment:
2016-08-02T19:16:06.622+0800 I CONTROL  [initandlisten]     distarch: x86_64
2016-08-02T19:16:06.622+0800 I CONTROL  [initandlisten]     target_arch: x86_64
2016-08-02T19:16:06.622+0800 I CONTROL  [initandlisten] options: {}
2016-08-02T19:16:06.622+0800 I STORAGE  [initandlisten] wiredtiger_open config: create,cache_size=4G,session_max=20000,eviction=(threads_max=4),config_base=false,statistics=(fast),log=(enabled=true,archive=true,path=journal,compressor=snappy),file_manager=(close_idle_time=100000),checkpoint=(wait=60,log_size=2GB),statistics_log=(wait=0),
2016-08-02T19:16:07.239+0800 I CONTROL  [initandlisten]
2016-08-02T19:16:07.239+0800 I CONTROL  [initandlisten] ** WARNING: soft rlimits too low. Number of files is 256, should be at least 1000
2016-08-02T19:16:07.239+0800 I FTDC     [initandlisten] Initializing full-time diagnostic data capture with directory '/data/db/diagnostic.data'
2016-08-02T19:16:07.239+0800 I NETWORK  [HostnameCanonicalizationWorker] Starting hostname canonicalization worker
2016-08-02T19:16:07.390+0800 I NETWORK  [initandlisten] waiting for connections on port 27017
```

+ 此时打开浏览器，输入下述地址：

```js
http://127.0.0.1:27017/
```
+ 出现如下所示的页面也代表启动成功。

```js
It looks like you are trying to access MongoDB over HTTP on the native driver port.
```









