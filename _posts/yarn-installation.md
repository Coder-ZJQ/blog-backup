---
title: Yarn Installation
date: 2016-10-13 13:28:17
categories: 
- Technology
- Tools
- Yarn
tags: [yarn]
---
## macOS

### Homebrew

你可以通过 [Homebrew package manager](http://brew.sh/)，这同时会安装 Node.js 如果没有安装的话。

``` bash
$ brew update
$ brew install yarn
```

### 设置 Path 环境变量

你需要通过你的终端设置 `Path` 环境变量，使 Yarn 的执行包可以全局访问。



在你的配置文件（可能是你的 `.profile`,`.bashrc`,`.zshrc`文件，等等。）里加入 `export PATH="$PATH:yarn global bin"`

<!-- more -->

## Windows

在 Windows 上有两种可选的方式来安装 Yarn。

### 下载安装包

下载安装包你会得到一个 `.msi` 文件，运行该文件会指引你安装 Yarn。



如果你通过安装包安装，你需先安装 [Node.js](https://nodejs.org/)。

<a style="color:white; background-color:#2c8ebb; border-color:#2c8ebb; display: inline-block; font-weight: normal; line-height: 1.25;text-align: center; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 1px solid transparent;  padding: .5rem 1rem; font-size: 1rem;  border-radius: .25rem;" href="https://yarnpkg.com/latest.msi">点击下载安装包</a>

### 通过 Chocolatey 安装

[Chocolatey](https://chocolatey.org/) 是 Windows 上的包管理工具，你可以通过[这里的指示](https://chocolatey.org/install)安装 Chocolatey.

如果你已经安装了 Chocolatey，你可以通过在你的命令行你运行如下代码来安装 Yarn:

``` bash
choco install yarn
```

这同样得确保你已经安装了 [Node.js](https://nodejs.org/).

### 注意

你需要清空你的文件夹以及防病毒软件里的 Yarn 缓存目录（ %LocalAppData%\Yarn ） ，否则安装包时会特别慢，因为每个文件在写入硬盘时都会被扫描。

---



可以在终端运行如下命令测试 Yarn 是否已安装成功：

``` bash
$ yarn --version
```

安装成功的话则会显示 Yarn 安装的版本信息：

![Yarn version](http://ofsuv8s64.bkt.clouddn.com/blog/2016-11-23-011736.jpg)

### 首先得安装 [Node.js](https://nodejs.org/)

### 最简单的通过脚本安装
``` bash
$ curl -o- -L https://yarnpkg.com/install.sh | bash
```
![QQ20161013-0.png](http://ww3.sinaimg.cn/large/65e4f1e6gw1f8ql5fz45bj20fu04rq56.jpg)

### npm
``` bash
$ npm install --global yarn
```

### Manual
You can install Yarn by [downloading a tarball](https://yarnpkg.com/latest.tar.gz) and extracting it anywhere.   
***OR***
``` bash
# install wget first
$ cd /opt
$ wget https://yarnpkg.com/latest.tar.gz
$ tar zvxf yarn-*.tar.gz
# Yarn is now in /opt/yarn-[version]/
```

### Test
``` bash
$ yarn --version
```
![13:42:18.jpg](http://ww1.sinaimg.cn/large/65e4f1e6gw1f8ql84cm8fj208x00q0ss.jpg)

### Uninstall
``` bash
$ rm -rf ~/.yarn
```

---
[Yarn Installation](https://yarnpkg.com/en/docs/install)

