---
title: Alcatraz 的安装与使用
date: 2016-04-22 22:25:48
categories: 
- Technology
- Tools
- Alcatraz
tags: 
- Alcatraz
---

### 什么是 Alcatraz ？
> Alcatraz is an open-source package manager for Xcode 7+. It lets you discover and install plugins, templates and color schemes without the need for manually cloning or copying files. It installs itself as a part of Xcode and it feels like home. 
> [Alcatraz](https://github.com/alcatraz/Alcatraz) 是一款在 Xcode 7+ 以上用于管理开源包的工具。它可以帮你查找或安装 Xcode 插件、模板、颜色主题，不需要认为的克隆或拷贝文件，它就像是 Xcode 的一部分。

<!-- more -->

**（注：Alcatraz 要求 Xcode 版本号为 7 以上）**

### Alcatraz 的安装
* 打开终端，在终端中输入：
``` bash
$ curl -fsSL https://raw.github.com/alcatraz/Alcatraz/master/Scripts/install.sh | sh
```
* 安装成功后显示如下，并重启 Xcode   
  ![安装](http://ww3.sinaimg.cn/large/006tNc79gw1f784eek7d0j30iy0dajue.jpg)
* 重启Xcode会提示你是否加载 Bundle，选择 ***Load Bundle***
* 按 `shift + command + 9` 或者 `Windows --> Package Manager` ，便可打开 Alcatraz 的图形界面

![图形界面](http://ww1.sinaimg.cn/large/006tNc79gw1f784ewdyxmj30i90hvq4y.jpg)

### Alcatraz 的卸载
* 打开终端，在终端中输入：
```bash
$ rm -rf ~/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins/Alcatraz.xcplugin
```

### Alcatraz 的使用
* 输入想要使用的插件，以 `KSImagedNamed` 为例，点击 **INSTALL** 便可安装   
  ![install](http://ww4.sinaimg.cn/large/006tNc79gw1f784f87k07j30i90j3dh7.jpg)
* 在项目中输入 `[UIImage imageNamed:]` 验证：   
  ![KSImagedNamed](http://ww1.sinaimg.cn/large/006tNc79gw1f784fo10mej30cj04kwfe.jpg)
* Alcatraz 安装的插件都会下载到 `~/Library/Application Support/Alcatraz/Plug-ins` 文件夹下   
  ![插件](http://ww1.sinaimg.cn/large/006tNc79gw1f784g01elmj305k0313yn.jpg)
* 因此若要删除不使用的插件，可直接在该文件夹下删除，或者在图形界面点击 **REMOVE** ，删除所有插件：
```bash
$ rm -rf ~/Library/Application\ Support/Alcatraz/
```
