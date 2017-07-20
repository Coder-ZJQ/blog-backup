---
title: SVN 常用指令
date: 2016-09-15 19:49:04
categories: 
- Technology
- Tools
- SVN
tags: [SVN]
---
### 基本使用
#### 帮助信息
``` bash
$ svn help
$ svn help help
```
<!-- more -->

#### 导入数据至你的远程版本库

- 导入文件和目录
``` bash
$ svn import [file-path] [svn-path] -m "[message]"
```
- 推荐的版本库布局
``` bash
$ svn list file:///var/svn/single-project-repo
trunk/
branches/
tags/
$ svn list file:///var/svn/multi-project-repo
project-A/
project-B/
$ svn list file:///var/svn/multi-project-repo/project-A
trunk/
branches/
tags/
```
#### 从远程版本库导出至本地工作区
``` bash
$ svn checkout [svn-path]
```
#### 更新工作区
``` bash
$ svn update
```
#### 修改工作区
``` bash
# 将文件或文件夹下文件添加至版本库，若只需添加文件夹可以使用 --depth=empth
$ svn add [file-path] | [dir-path]
# 从版本库删除
$ svn delete [file-path] | [dir-path]
# 
$ svn copy
$ svn move
$ svn mkdir 
```
#### 查看修改
``` bash
$ svn status
$ svn status [file-path]
$ svn status -v
$ svn status -u -v
```
#### 查看修改详情
``` bash
$ svn diff
$ svn diff > patchfile
```
#### 恢复修改
``` bash
$ svn revert
```
####