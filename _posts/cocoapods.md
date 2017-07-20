---
title: CocoaPods 的安装与使用
date: 2016-04-22 21:00:07
categories: 
- Technology
- Tools
- CocoaPods
tags: 
- CocoaPods
---
### 什么是 CocoaPods？
> CocoaPods 可以为你管理 Xcode 项目中使用的依赖库，且只需要编辑一个简单的文本文件—— Podfile 。CocoaPods 会解析这些库之间的依赖，获取源代码，并将它们放入一个 Xcode 工作空间，以可以被用来构造你的项目。

<!-- more -->

### CocoaPods 的安装
> CocoaPods 是以 Ruby 构建的，幸运的是 Mac OS X 自带默认的 Ruby 环境，因此安装很简单，不过需先更换下 Ruby 的默认源（被墙）。    

![Ruby源.png](http://ww4.sinaimg.cn/large/801b780agw1f6yph89faqj20b203y3z7.jpg)

* 移除 Ruby 默认源：
``` bash
$ gem sources --remove https://rubygems.org/
```
* 添加国内淘宝提供的 Ruby 源（注：已经换成 https 协议的）：
``` bash
$ gem sources -a https://ruby.taobao.org/
```
* 查看是否替换成功，并且确定只有 `https://ruby.taobao.org/` 这一个源：
``` bash
$ gem sources -l:
```
* 若显示如下则表示替换成功：
``` bash
*** CURRENT SOURCES *** 

https://ruby.taobao.org/
```
* 安装 CocoaPods 至:
``` bash
$ sudo gem install cocoapods(OS X 10.11之前)
$ sudo gem install -n /usr/local/bin cocoapods (OS X 10.11之后)
```
* 输入密码，安装成功后接着执行，设置 CocoaPods 的环境
``` bash
$ pod setup
```
* 之后便会在 `/usr/local/bin` 或 `/usr/bin` 文件夹下看到这些可执行文件：   
  ![pod](http://ww4.sinaimg.cn/large/801b780agw1f6yphqwe4jj204p02omxa.jpg)
* 可以查看下 CocoaPods 版本验证是否安装成功
``` bash
$ pod --version
```


### 终端使用CocoaPods
* 新建一个 Xcode 项目
* cd 到项目根目录下：
``` bash
$ cd /Users/Joker/Desktop/TestPods/ 
```
* 创建 Podfile
``` bash
$ touch Podfile
```
* 使用 vim 编辑 Podfile
``` bash
$ vim Podfile
```
* 输入如下内容，并 `:wq` 保存退出   
``` bash 
# 表示使用平台是iOS
platform:ios
# 导入AFNetworking，没有标明版本的话，默认是导入最新版
pod 'AFNetworking'
```
* 开始安装需导入的依赖库
``` bash
$ pod install
```
* 导入成功的话会提示你以后使用 `XXXX.xcworkspace` 文件打开项目    
```
[!] Please close any current Xcode sessions and use 
TestPods.xcworkspace for this project from now on.
```
  ![安装成功](http://ww3.sinaimg.cn/large/801b780agw1f6ypie1flhj20fr07ut9x.jpg)
* 且项目根目录下会自动生成一些文件   
  ![项目根目录](http://ww1.sinaimg.cn/large/801b780agw1f6ypio6z7kj20520450sy.jpg)
* 打开项目，此时项目下有两个工作空间，新增的则为 CocoaPods 用以管理依赖库的工作空间，可在该工作空间的 Pods 文件夹下看到导入的依赖库   
  ![项目文件结构](http://ww4.sinaimg.cn/large/801b780agw1f6ypiwmb2ij205404g74g.jpg)


### 利用 CocoaPods 插件
***除了利用终端使用 CocoaPods 之外，还可以为 Xcode 安装 CocoaPods 插件，使 pod 更加简单。***

* 下载 [kattrali/cocoapods-xcode-plugin](https://github.com/kattrali/cocoapods-xcode-plugin)
* 打开 `CocoaPods.xcworkspace` 运行，便可在 `~/Library/Application Support/Developer/Shared/Xcode/Plug-ins/` 文件夹下看到 CocoaPods 插件   
  ![cocoapods-xcode-plugin](http://ww2.sinaimg.cn/large/801b780agw1f6ypj8v2tlj2056069mx9.jpg)
* 从 Xcode 5 开始，苹果要求加入 UUID 证书从而保证插件的稳定性。因此Xcode版本更新之后需要在 `cocoapods-xcode-plugin` 的 `Info.plist` 文件中添加 Xcode 的 UUID 。终端下输入：
``` bash
$ defaults read /Applications/Xcode.app/Contents/Info 
DVTPlugInCompatibilityUUID
```
* 在 `~/Library/Application Support/Developer/Shared/Xcode/Plug-ins/` 文件夹下找到 CocoaPods 插件，显示包内容，并在 info.plist 中的 `DVTPlugInCompatibilityUUIDs` 项新增刚才获取的 UUID ：   
  ![info.plist](http://ww2.sinaimg.cn/large/801b780agw1f6ypjiusrvj208g08x3z7.jpg)
* 添加成功后重启Xcode便会提示，选择 ***Load Bundle***   
  ![Load Bundle](http://ww4.sinaimg.cn/large/801b780agw1f6ypjsp0d7j20es08bgmd.jpg)
* 此时打开Xcode项目便可在 Product 下看到：   
  ![CocoaPods](http://ww1.sinaimg.cn/large/801b780agw1f6ypk4x81kj20cb092ab6.jpg)
* 记得修改 GEM_PATH 为 CocoaPods 的安装目录，如：/usr/local/bin
* 之后使用 CocoaPods pod依赖库便是可视化的
```
Create/Edit Podfile:创建或编辑Podfile
Install Pods:安装
Update Pods:更新
```


### 附：   
1. pod 常用命令：
``` 
pod install: 安装依赖库，并将版本信息写入 Podfile.lock 文件；
pod plugins:查看可用的 CocoaPods 插件；
pod list:查看远程 pods 库中所有的依赖库；
pod search:查找需导入的依赖库是否在 pods 库中；
pod setup:设置 CocoaPods 的环境；
pod update:更新过期的依赖库，并且创建新的 Podfile.lock 文件；
pod --version: 查看工具版本号；
pod --help:显示帮助信息。
```
2. pod 控制依赖库版本：
``` 
//不显式指定依赖库版本，表示每次都获取最新版本
pod ‘AFNetworking’
//只使用2.0版本
pod ‘AFNetworking’,  ‘2.0’
//使用高于2.0的版本
pod ‘AFNetworking’, ‘>2.0′
//使用大于或等于2.0的版本
pod ‘AFNetworking’, ‘>=2.0′
//使用小于2.0的版本
pod ‘AFNetworking’, ‘<2.0′
//使用小于或等于2.0的版本
pod ‘AFNetworking’, ‘<=2.0′
//使用大于等于0.1.2但小于0.2的版本，相当于>=0.1.2并且<0.2.0
pod ‘AFNetworking’, ‘~>0.1.2′
//使用大于等于0.1但小于1.0的版本
pod ‘AFNetworking’, ‘~>0.1′ 
//高于0的版本，写这个限制和什么都不写是一个效果，都表示使用最新版本 
pod ‘AFNetworking’, ‘~>0′     
```

