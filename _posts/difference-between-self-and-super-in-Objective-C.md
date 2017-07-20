---
title: Objective-C 中 self 与 super 的区别
date: 2016-08-16 20:42:26
categories: 
- Technology
- Programming
- Objective-C
tags: 
- self
- super
---
### 以下代码的打印结果是什么？为什么？
``` objc
@interface JQApple : JQFruit
@end

@implementation JQApple
- (instancetype)init{
    self = [super init];
    if (self) {
        NSLog(@"%@", NSStringFromClass([self class]));
        NSLog(@"%@", NSStringFromClass([super class]));
    }
    return self;
}
@end
```

<!-- more -->

按照面向对象的思想应该是分别打印`JQApple`和`JQFruit`
然而运行结果却出乎我们的意料，最终均都打印“JQApple”。这是为什么？

因为`self`是类的隐藏参数，指向当前调用方法的对象。而`super`并不是如我们所想是指向当前对象父类的指针。其实`super`是一个编译器标识符，在运行时中与`self`相同，指向同一个消息接受者，只是`self`会优先在当前类的`methodLists`中查找方法，而`super`则是优先从父类中查找。验证如下：   
在终端运行：
``` bash
 $ clang -rewrite-objc main.m
```
可以看到运行时代码如下：
``` objc
NSLog((NSString *)&__NSConstantStringImpl__var_folders_ld_03322m393b5cyvhz2zhv2c100000gn_T_main_97554f_mi_0, NSStringFromClass(((Class (*)(id, SEL))(void *)objc_msgSend)((id)self, sel_registerName("class"))));
NSLog((NSString *)&__NSConstantStringImpl__var_folders_ld_03322m393b5cyvhz2zhv2c100000gn_T_main_97554f_mi_1, NSStringFromClass(((Class (*)(__rw_objc_super *, SEL))(void *)objc_msgSendSuper)((__rw_objc_super){(id)self, (id)class_getSuperclass(objc_getClass("JQApple"))}, sel_registerName("class"))));
```
删除相关无关类型及方法后代码如下：
``` objc
objc_msgSend((id)self, sel_registerName("class"));
objc_msgSendSuper((__rw_objc_super){(id)self, (id)class_getSuperclass(objc_getClass("JQApple"))}, sel_registerName("class"));
```
查看函数定义：
``` objc
/** 
 * Sends a message with a simple return value to an instance of a class.
 * 
 * @param self A pointer to the instance of the class that is to receive the message.
 * @param op The selector of the method that handles the message.
 * @param ... 
 *   A variable argument list containing the arguments to the method.
 * 
 * @return The return value of the method.
 * 
 * @note When it encounters a method call, the compiler generates a call to one of the
 *  functions \c objc_msgSend, \c objc_msgSend_stret, \c objc_msgSendSuper, or \c objc_msgSendSuper_stret.
 *  Messages sent to an object’s superclass (using the \c super keyword) are sent using \c objc_msgSendSuper; 
 *  other messages are sent using \c objc_msgSend. Methods that have data structures as return values
 *  are sent using \c objc_msgSendSuper_stret and \c objc_msgSend_stret.
 */
OBJC_EXPORT id objc_msgSend(id self, SEL op, ...)
    __OSX_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
/** 
 * Sends a message with a simple return value to the superclass of an instance of a class.
 * 
 * @param super A pointer to an \c objc_super data structure. Pass values identifying the
 *  context the message was sent to, including the instance of the class that is to receive the
 *  message and the superclass at which to start searching for the method implementation.
 * @param op A pointer of type SEL. Pass the selector of the method that will handle the message.
 * @param ...
 *   A variable argument list containing the arguments to the method.
 * 
 * @return The return value of the method identified by \e op.
 * 
 * @see objc_msgSend
 */
OBJC_EXPORT id objc_msgSendSuper(struct objc_super *super, SEL op, ...)
    __OSX_AVAILABLE_STARTING(__MAC_10_0, __IPHONE_2_0);
```
可知`objc_msgSend`函数中的`self`参数是指指向接收消息的类的实例的指针，即消息接受者，而`op`参数则是指处理该消息的`selector`；`objc_msgSendSuper`函数中的参数`super`则是一个`objc_super`结构体，`objc_super`结构体定义如下：
``` objc
/// Specifies the superclass of an instance. 
struct objc_super {
    /// Specifies an instance of a class.
    __unsafe_unretained id receiver;

    /// Specifies the particular superclass of the instance to message. 
    __unsafe_unretained Class super_class;

    /* super_class is the first class to search */
};
```
其中`receiver`是指类的实例，`super_class`则是指该实例的父类。可以看到在编译后的`C++`代码中有个`__rw_objc_super`结构体：
``` objc
struct __rw_objc_super { 
    struct objc_object *object; 
    struct objc_object *superClass; 
    __rw_objc_super(struct objc_object *o, struct objc_object *s) : object(o), superClass(s) {} 
};
```
其实即为`objc_super`结构体。通过`(__rw_objc_super){(id)self, (id)class_getSuperclass(objc_getClass("JQApple"))}`该段代码可知：我们把`self`以及`JQApple`的父类通过结构体的构造方法构造了一个`__rw_objc_super`结构体，也就是`objc_super`。因此`objc_super`结构体中的`receiver`既是`self`。所以`[self class]`和`[super class]`指向的是同一个消息接受者，只是`self`会优先从当前类的实现中寻找方法处理消息，而`super`则是会优先从`objc_super`结构体中的`super_class`也就是父类的实现中查找。`JQFruit`及`JQApple`中均未实现`- (Class)class;`方法，因此会逐级向上查找最终调用基类`NSObject`的`- (Class)class;`方法，通过官方开源的`NSObject`的`- (Class)class;`方法代码：
``` objc
- (Class)class{
    return object_getClass(self);
}
```
可知，消息接受者是`self`，而`[self class]`和`[super class]`指向的是同一个消息接受者，因此该段代码均打印`JQApple`。
