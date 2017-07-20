---
title: ＠property 、 ＠synthesize 与 ＠dynamic 的作用
date: 2016-08-09 08:32:13
categories: 
- Technology
- Programming
- Objective-C
tags:
- ＠property
- ＠synthesize
- ＠dynamic
---
- **@property**: 用于声明成员变量的 getter/setter 方法
- **@synthesize**: 与 @property 配套使用，@synthesize 会自动生成一个`_`开头的成员变量（若是不指定的话），并实现 @property 声明的 getter/setter 方法。
- **@dynamic**: 不会自动生成成员变量，程序员需自己添加成员变量并实现 getter/setter 方法。    

<!-- more -->

** 具体细节详见以下代码：**

``` objc
#import <Foundation/Foundation.h>

@interface JQPerson : NSObject
{
    //  3.1 由于 @dynamic 并不会自动生成成员变量，因此需自主添加成员变量用于 getter/setter 方法，否则会报 “Use undeclared identifier” 错误。
    NSInteger _weight;
}

//  1. @property 的简单使用
@property (nonatomic, copy) NSString *name;
@property (nonatomic, assign) NSInteger age;
@property (nonatomic, assign) NSInteger height;
@property (nonatomic, assign) NSInteger weight;

@end

@implementation JQPerson

//  2. @synthesize 的使用
//  2.1 默认生成"_"开头的成员变量， 即：
@synthesize name = _name;
//  2.2 生成与 @property 相同的不带下划线的成员变量：
@synthesize age;
//  2.3 指定生成的成员变量名：
@synthesize height = H;

//  3. @dynamic 的使用
@dynamic weight;
//  3.2 实现 getter/setter 方法（这里只是简单的实现）：
- (void)setWeight:(NSInteger)weight {
    _weight = weight;
}
- (NSInteger)weight {
    return _weight;
}

@end
```
***（Tips：在都没有使用 @synthesize 以及 @dynamic 时，默认为 `@synthesize propertyName = _propertyName;`。但若是同时实现了 getter&setter 方法，则隐含表示为 `@dynamic propertyName;` 因此编译器并不会自动生成成员变量，此时若是使用成员变量则会出现 “Use undeclared identifier” 错误。解决方法可以在类的声明中自主添加私有的成员变量，或者使用 @synthesize，告知编译器自动生成成员变量。）***
