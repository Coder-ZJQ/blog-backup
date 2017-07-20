---
title: RN(1) Build The Environment
date: 2016-10-02 20:42:26
categories: 
- Technology
- Programming
- React Native
tags: 
- React Native
---
### 搭建开发环境
* 安装 Homebrew 以搭建 Node 环境
``` bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
* 利用 Homebrew 安装 Node
``` bash
$ brew install node
```
* 安装 watchman
``` bash
$ brew link pcre
$ brew install watchman
```
<!-- more -->
* 安装 React Native 命令行工具：react-native-cli
``` bash
$ npm install -g react-native-cli
```
* 运行项目
``` bash
# 利用安装的 react-native-cli 初始化项目
$ react-native init MyFirstReactNativeProject
# 进入项目目录
$ cd MyFirstReactNativeProject
# 运行项目
$ react-native run-ios
```
![15:40:37.jpg](http://ww4.sinaimg.cn/large/801b780agw1f8f4g5mg9hj20g90a6jtd.jpg)
![15:40:54.jpg](http://ww4.sinaimg.cn/large/801b780agw1f8f4gfp9vyj20af0j50t6.jpg)
