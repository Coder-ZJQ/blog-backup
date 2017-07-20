---
title: SVN 的简单使用
date: 2016-09-08 09:55:09
categories: 
- Technology
- Tools
- SVN
tags: [SVN]
---
### 创建代码库
``` bash
$ svnadmin create /Users/Joker/svn/MyRepo
```

<!--more-->

### 设置代码库权限以及相关配置
修改代码库文件夹下的 `conf/svnserve.conf` 文件
``` bash
$ vi /Users/Joker/svn/MyRepo/conf/svnserve.conf
```

删除以下几项前的 `#` 号，表示代码库可读可写，用户密码等配置在 `passwd` 文件，授权信息在 `authz` 文件
```
# anon-access = read  
# auth-access = write  
# password-db = passwd  
# authz-db = authz 
```

### 配置用户密码等信息
编辑代码库文件夹下的 `conf/passwd` 文件
``` bash
$ vi /Users/Joker/svn/MyRepo/conf/passwd
```
在 `[users]` 标签下添加用户信息，表示账号为：zjq，密码为：123
```
[users]
zjq = 123
```

### 配置用户组或用户权限
编辑代码库文件夹下的 `conf/authz` 文件
``` bash
$ vi /Users/Joker/svn/MyRepo/conf/authz
```
可以将若干用户分为一组，统一配置权限，`[/]` 表示代码库下所有文件，`rw` 表示可读可写
```
[groups]
group1 = zjq, joker

[/]
@group1 = rw
```
也可以单独给用户配置权限，注意给用户单独配置权限不需要 `@`
```
[/]
zjq = rw
```

### 启动 SVN 服务器
``` bash
$ svnserve -d -r /Users/Joker/svn/MyRepo
```

### 使用 SVN
#### 从本地导入代码至服务器
``` bash
$ svn import [file-path] [server-path] --username=zjq --password=123 -m "initialize"
```
#### 从服务器下载代码至本地代码库
``` bash
$ svn checkout [server-path] --username=zjq --password=123 [repo-path] 
```
#### 提交修改至服务器
``` bahs
$ svn commit -m "modified the file"
```
#### 更新服务器代码至本地代码库
``` bash
$ svn update
```
#### 查看帮助信息
``` bash
$ svn help
```
