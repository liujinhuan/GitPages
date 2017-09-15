---
title: 新Mac的装机过程
date: 2017-9-15 22:47:12
tags: 
	- Mac
---
> 2017年9月11日新入职一家公司。15寸+最高配带TouchBar的Pro已经分配到了我这里。装机的过程是痛苦的，因为打开电脑后，啥也没有。那就来个记录，免得以后遗忘。

### Chrome(前端开发🐶的缘故，钟爱Chrome)

+ Safiri搜索Chrome，选择Mac下载。
![ChromeInstall](https://raw.githubusercontent.com/liujinhuan/StaticResource/master/images/Install-Mac/chrome-install.png)

### 微信+QQ+QQ音乐

<!-- more  -->

+ AppStore登录账号，搜索安装即可

### Office 破解版

+ 从同事那里获得一个`pkg`和`破解补丁.dmg`。[点击下载](http://www.baidu.com)。安装时先安装pkg，安装完成后，先不要点击各个office，紧接着安装破解补丁.dmg，安装后在登录，就是可以跳过登录的破解版了。

### SourceTree 破解版

+ [还未上传百度网盘连接](http://www.baidu.com)

### SublimeText

+ Safiri搜索Chrome，选择Mac下载。
![SublimeInstall](https://raw.githubusercontent.com/liujinhuan/StaticResource/master/images/Install-Mac/sublime-install.png)

+ 安装后，需要设置字体。打开sublime，依次点击菜单栏`SublimeText->Preferences->seeting-user`，输入以下配置，保存：

```js
{
  "font_face": "Courier New",
  "font_size": 17
}
```

### ShadowsocksX-2.6.3

+ [百度下载](https://zh.osdn.net/projects/sfnet_shadowsocksgui/downloads/dist/ShadowsocksX-2.6.3.dmg/).


### Node

+ [官网下载](https://nodejs.org/en/download/)。安装过程中，记得选中`Make sure that /usr/local/bin is in your $PATH.
+ Node安装后，是再带npm包管理器的。需要设置淘宝镜像

```
设置淘宝镜像：npm config set registry https://registry.npm.taobao.org

设置为原镜像：npm config set registry http://registry.npmjs.org  
```

### Git+xCode

+ AppStore登录账号，搜索安装xCode即可.Git为xCode自带。安装之后命令行查看git版本即可。
```
➜  ~ git version
git version 2.11.0 (Apple Git-81)
```

### iTerm2+zsh

+ [官网下载iTerm2](http://www.iterm2.com/).按照步骤安装即可。
+ 打开iTerm2，依次点击`iterm2->Perfernce->Profile`，左下角新建`Profile`并命名如：myzsh。
+ 任意目录新建文件`Monokai-Soda.itermcolors`,[点击见详细内容](https://raw.githubusercontent.com/tofishes/iterm2-zsh/master/_zshrc)
+ 步骤2中的新Profile-myzsh，右侧点击color，右下角点击`color presets`，选择`import`刚刚步骤3中创建的文件。记得：左侧点击`save defaults`

![字体设置](https://raw.githubusercontent.com/liujinhuan/StaticResource/master/images/Install-Mac/iterm2-1.png)
![字号设置](https://raw.githubusercontent.com/liujinhuan/StaticResource/master/images/Install-Mac/iterm2-2.png)
![窗口及透明度设置](https://raw.githubusercontent.com/liujinhuan/StaticResource/master/images/Install-Mac/iterm2-3.png)

+ 关闭窗口，重启iTerm2。新建tab，输入如下地址，并输入开机密码，完成安装zsh。
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
![zsh安装](https://raw.githubusercontent.com/liujinhuan/StaticResource/master/images/Install-Mac/zsh-install.png)

+ 关闭窗口，重启iTerm2。发现上方已经变成zsh。
![zsh展示](https://raw.githubusercontent.com/liujinhuan/StaticResource/master/images/Install-Mac/zsh-show.png)


