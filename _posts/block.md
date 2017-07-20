---
title: block 的使用
date: 2016-08-27 14:02:21
categories: 
- Technology
- Programming
- Objective-C
tags: 
- block
---
### 前言
- `return_type`：你所想要返回的数据类型；
- `blockName`：你所构造的 block 名；
- `var_type`：你所要传递的变量类型；
- `varName`：你所要传递的变量名。

<!-- more -->

（另外参数可以传入多个）

### 作为变量
``` objc
return_type (^blockName)(var_type) = ^return_type (var_type varName)
{
    // Your code here...
};
```
### 作为属性
``` objc
@property (copy) return_type (^blockName) (var_type);
```
### 作为方法定义参数
``` objc
- (void)yourMethod:(return_type (^)(var_type))blockName;
```
### 作为方法传入参数
``` objc
[someObject doSomethingWithBlock: ^return_type (var_type varName)
{
    // Your code here...
}];
```
### 匿名 Block
``` objc
^return_type (var_type varName)
{
    // Your code here...
};
```
### 使用 `typedef`
``` objc
typedef return_type (^blockName)(var_type);
```
### 内联 Block
``` objc
^return_type (var_type varName)
{
    // Your code here...
}(var);
```
### 递归 Block
``` objc
__block return_type (^blockName)(var_type) = [^return_type (var_type varName)
{
    if (returnCondition)
    {
        blockName = nil;
        return;
    }

    // Your code here...
} copy];
blockName(varValue);
```
### 作为返回值
``` objc
- (return_type(^)(var_type))methodName
{
    // Your code here...
}
```
### 在 swift 中
``` swift
blockName = (varName: var_type) -> (return_type)
```