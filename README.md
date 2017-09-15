# GitPagesWWW

### cd到根目录

```
cd Documents/GitHub/GitPagesWWW/
```

### 安装依赖

```
npm install
```

### 本地服务

```
hexo server
```

### 本地编译

```
hexo g
```

### copy

```
拷贝生成的public文件内容到博客根目录下，全部替换。git-commit。
```

# 小坑

### 新入司，换了最高配的Pro。发现该项目跑不起来了。怀疑是hexo的版本更新导致。索性采用如下方式：

```
npm install hexo -g 安装最高版本hexo，此时是3.3.9。
hexo init 初始化hexo目录
hexo server 本地服务4000端口
hexo g 编译文件，这时可以看出public目录和以前大不一样。
```