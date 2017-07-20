---
title: LLDB — 让调试更有趣
date: 2016-08-19 07:41:06
categories: 
- Technology
- Debug
- LLDB
tags: 
- LLDB
---

### 什么是 [LLDB](http://lldb.llvm.org)？
* LLDB 是一个有着 REPL（交互式）的特性和 C++ ，Python 插件的开源调试器；
* LLDB 是 Xcode 中默认的调试器，支持在桌面、iOS 设备以及 iOS 模拟器上调试以 C 语言、Objective-C 或者 C ++ 编写的程序；
* LLDB 允许你在程序运行的特定时暂停它，你可以查看变量的值，执行自定的指令，并且按照你所认为合适的步骤来操作程序的进展。

<!-- more -->

---

### LLDB 简单使用
在此之前你可能已经使用过 LLDB ，也许只是在 Xcode 的界面上加一些断点，查看一些变量的值。但是通过一些小的技巧，你就可以做一些非常酷的事情。

#### *help* — 指令帮助
`help` 是最简单的指令，输入 `help`便会为你列举所有的命令。同时，如果你忘记一条指令的作用或者想要知道更多，你便可以输入 `help <command>` 其中 `<command>` 为你想要了解的指令，例如： `help print`。

![help](http://ww1.sinaimg.cn/large/801b780agw1f6ypwim8rpj20ex0693zy.jpg)

![help print](http://ww4.sinaimg.cn/large/801b780agw1f6ypwwtyzbj20eo01lq3c.jpg)


#### *p* & *po* — 打印变量或者对象
因为 LLDB 支持前缀匹配，因此你可以将 `print` 简写为 `p` 或者 `pri` ，而 `print` 则代表 `expression --` ；`po` 则代表 `expression -O --` ，意为 print object ，打印对象。
输入 `p` 指令可打印其对象类型、内存地址以及该对象的值等具体信息，而 `po` 指令则是打印其调用 `description` 方法得到的值。

*(注：打印集合类型对象时，`p`指令会省略具体的值，只提示集合的数量等信息，因此若需查看集合中的值应使用 `po`指令，如下图所示：)*   

##### 打印 NSString :   
![p & po NSString](http://ww3.sinaimg.cn/large/801b780agw1f6ypyaz7pzj20b801i74i.jpg)

##### 打印 NSDictionary :   
![p & po NSDictionary](http://ww2.sinaimg.cn/large/801b780agw1f6ypyjfpuzj20bk02oq37.jpg)

##### 打印 Person :   
``` objc
#import <Foundation/Foundation.h>

#pragma mark - 自定义Person类
@interface Person : NSObject
/** 名字 */
@property (nonatomic, copy) NSString *name;
/** 年龄 */
@property (nonatomic, assign) NSInteger age;
@end

@implementation Person
/** 重写description方法 */
- (NSString *)description{
    return [NSString stringWithFormat:@"name:%@,age:%ld", self.name, self.age];
}
@end

#pragma mark - main函数
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Person *p = [[Person alloc] init];
        p.name = @"Joker";
        p.age = 23;
    }
    return 0;
}
```

![p & po Person](http://ww2.sinaimg.cn/large/801b780agw1f6ypytojm9j207301kt8u.jpg)

##### 指定格式打印：   
* 以二进制打印
``` lldb
(lldb) p/t 23
(int) $0 = 0b00000000000000000000000000010111
```
* 以八进制打印
``` lldb
(lldb) p/o 23
(int) $1 = 027
```
* 以十六进制打印
``` lldb
(lldb) p/x 23
(int) $2 = 0x00000017
```
* 以二进制打印，且只打印一个字节即八位(char类型只占据一个字节的内存)
``` lldb
(lldb) p/t (char)23
(char) $3 = 0b00010111
```

---

#### *expression* — 改变值

如果你想在调试的时候改变一个已有的值，那么你可以使用`expression`指令，也可以简写为`e`

* 在打印前添加断点：   
![添加断点](http://ww4.sinaimg.cn/large/801b780agw1f6yr04sauoj209202qq35.jpg)

* 利用LLDB查看并修改已经定义的值：   
![查看并修改](http://ww4.sinaimg.cn/large/801b780agw1f6yqzvlh51j20cr030aal.jpg)

* 继续运行查看打印结果   
![查看打印](http://ww4.sinaimg.cn/large/801b780agw1f6yqzo0t8wj20bx00sjrk.jpg)

可以看到之前定义的值通过LLDB已经成功被修改了。

---
### LLDB更新UI
既然LLDB可以修改已定义的值，那么LLDB能否在调试时修改UI中各类控件属性，以实现在不重新运行程序的情况下，更新UI查看效果？接下来进行验证：

* 新建一个iOS项目，运行并断点，查看当前界面效果   
![原始界面](http://ww1.sinaimg.cn/large/801b780agw1f6yqzfn33qj20c00ji3yw.jpg)

* LLDB中改变控制器view背景   
![LLDB更新UI](http://ww1.sinaimg.cn/large/801b780agw1f6yqz6tqduj20bg01idg5.jpg)

* 界面已经更新，变为绿色   
![改变界面](http://ww1.sinaimg.cn/large/801b780agw1f6yqyvmxt6j20c00ji3yz.jpg)