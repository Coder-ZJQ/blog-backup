---
title: swift 基本运算符
date: 2016-08-19 14:44:54
categories: 
- Technology
- Programming
- swift
tags:
- Basic Operators
---
#### 如果赋值运算的右边是一个包含多个值的元组，则它的元素会被一次分成多个常量或变量：

``` swift
let (x, y) = (1, 2)
// x则等于1，y则等于2
```

<!-- more -->

#### 不同于C及Objective-C中的赋值运算符，在Swift中的赋值运算符并不会返回值，因此以下表达式是错误的：

``` swift
if x = y {
    // 这是错误的，因为x = y并不会返回一个值
}
```

#### 浮点数求余运算：不同于C及Objective-C中的求余运算，Swift的求余运算还可以运算浮点数：

``` swift
8 % 2.5    // 等于0.5
// 在这个例子中8除以2.5等于3，余0.5，因此求余运算符返回0.5的Double型。
```

#### 元组也可比较运算，元组的比较运算从左至右，每次比较一个值，直到找到两个值不相等。如果所有元素都相等，则表示元组相等，例如：

``` swift
(1, "zebra") < (2, "apple")   // true，因为1小于2
(3, "apple") < (3, "bird")    // true，因为3等于3，但是"apple"小于"bird"
(4, "dog") == (4, "dog")      // true，因为4等于4，且"dog"等于"dog"
```
**注意：**   
swift标准库中的元组比较运算只支持少于7个元素的元组比较，若是要比较7个或更多元素的元组则需要你自己重载比较运算符。

#### 空合并运算符(Nil Coalescing Operator)

空合并运算符(`a ?? b`)会对可选值`a`解包如果它有值的话，如果`a`是`nil`的话，则会返回一个默认的值`b`，表达式中的`a`一般为可选类型，而`b`必须与`a`的存储类型相匹配。

空合并运算符可速记为如下代码：
``` swift
a != nil ? a! : b
```
上述代码利用三目运算符，当`a`不为`nil`时将`a`强制解包(`a!`)读取`a`中的值，否则则返回默认值`b`。空合并运算符提供了一种更为优雅的方式来处理条件判断及解包操作，更加简洁，更具阅读性。
**注意：**   
如果a的值非空，则b的值不会被估值，这就是所谓的短路求值。

下面的例子利用空合并运算符，在默认的颜色名以及可选的用户定义颜色名之间选择：

``` swift
let defaultColorName = "red"
var userDefinedColorName: String?   // userDefinedColorName默认为nil
var colorNameToUse = userDefinedColorName ?? defaultColorName
// 因为userDefinedColorName为nil，因此colorNameToUse将会赋值为"red"
```
