---
title: MJExtension 的使用
date: 2016-09-06 14:42:31
categories: 
- Technology
- Programming
- Objective-C
tags: 
- MJExtension
- JSON
---
### Define the models
``` objc
// Define JQPerson model
#import <Foundation/Foundation.h>
@class JQChild;

typedef NS_ENUM(NSInteger, JQSex) {
    JQSexMale = 0,
    JQSexFemale,
    JQSexUnknown
};

@interface JQPerson : NSObject

@property (nonatomic, copy) NSString *name;
@property (nonatomic, assign) NSInteger age;
@property (nonatomic, assign) JQSex sex;
@property (nonatomic, copy) NSString *address;
@property (nonatomic, assign, getter=isMarried) BOOL marriage;
@property (nonatomic, strong) JQChild *child;

@end

/**************************************************************/

// Define JQChild model
#import <Foundation/Foundation.h>

@interface JQChild : NSObject

@property (nonatomic, copy) NSString *name;
@property (nonatomic, assign) NSInteger age;

@end
```
<!--more-->
### JSON -> Model: `+ mj_objectWithKeyValues`
``` objc
// Define a JSON dictionary
NSDictionary *personDict = @{
                                 @"name":@"zjq",
                                 @"age":@(24),
                                 @"sex":@(JQSexMale),
                                 @"address":@"FuZhou",
                                 @"marriage":@"false"
                                 };

// JSON -> JQPerson
JQPerson *person = [JQPerson mj_objectWithKeyValues:personDict];

// Print
NSLog(@"name:%@, age:%ld, sex:%ld, address:%@, marriage:%d.", person.name, person.age, person.sex, person.address, person.marriage);
// name:zjq, age:24, sex:0, address:FuZhou, marriage:0.
```
### JSONString -> Model: `+ mj_objectWithKeyValues`
``` objc
// Define a JSON string
NSString *personStr = @"{\"name\":\"zjq\", \"age\":24, \"sex\":0, \"address\":\"FuZhou\", \"marriage\":\"false\"}";

// JSONString -> Model
JQPerson *person = [JQPerson mj_objectWithKeyValues:personDict]; 

// Print   
NSLog(@"name:%@, age:%ld, sex:%ld, address:%@, marriage:%d.", person.name, person.age, person.sex, person.address, person.marriage);
// name:zjq, age:24, sex:0, address:FuZhou, marriage:0.
```
### Model contains model: `+ mj_objectWithKeyValues`
``` objc
// Define a JSON dictionary
NSDictionary *personDict = @{
                                 @"name":@"zjt",
                                 @"age":@(31),
                                 @"sex":@(JQSexMale),
                                 @"address":@"FuZhou",
                                 @"marriage":@"true",
                                 @"child":@{
                                         @"name":@"zje",
                                         @"age":@(2)
                                         }
                                 };

// JSON -> JQPerson
JQPerson *person = [JQPerson mj_objectWithKeyValues:personDict];  

// Print 
NSLog(@"name:%@, age:%ld, sex:%ld, address:%@, marriage:%d, childname:%@, childage:%ld.", person.name, person.age, person.sex, person.address, person.marriage, person.child.name, person.child.age);
// name:zjt, age:31, sex:0, address:FuZhou, marriage:1, childname:zje, childage:2.
```
### Model -> JSON: `- mj_keyValues`
``` objc
// New model
User *user = [[User alloc] init];
user.name = @"Jack";
user.icon = @"lufy.png";

Status *status = [[Status alloc] init];
status.user = user;
status.text = @"Nice mood!";

// Status -> JSON
NSDictionary *statusDict = status.mj_keyValues;
NSLog(@"%@", statusDict);
/*
 {
 text = "Nice mood!";
 user =     {
 icon = "lufy.png";
 name = Jack;
 };
 }
 */

// More complex situation
Student *stu = [[Student alloc] init];
stu.ID = @"123";
stu.oldName = @"rose";
stu.nowName = @"jack";
stu.desc = @"handsome";
stu.nameChangedTime = @"2018-09-08";

Bag *bag = [[Bag alloc] init];
bag.name = @"a red bag";
bag.price = 205;
stu.bag = bag;

NSDictionary *stuDict = stu.mj_keyValues;
NSLog(@"%@", stuDict);
/*
{
    ID = 123;
    bag =     {
        name = "\U5c0f\U4e66\U5305";
        price = 205;
    };
    desc = handsome;
    nameChangedTime = "2018-09-08";
    nowName = jack;
    oldName = rose;
}
 */
```
### Model contains model array: `+ mj_objectClassInArray; + mj_setupObjectClassInArray:;`
``` objc
// Change The child model to childs array
@interface JQPerson : NSObject

@property (nonatomic, copy) NSString *name;
@property (nonatomic, assign) NSInteger age;
@property (nonatomic, assign) JQSex sex;
@property (nonatomic, copy) NSString *address;
@property (nonatomic, assign, getter=isMarried) BOOL marriage;
@property (nonatomic, strong) NSArray *childs;

@end

// JQPerson.m implements +mj_objectClassInArray method to tell MJExtension what type model will be contained in childs
+ (NSDictionary *)mj_objectClassInArray {
    return @{
             @"childs":@"JQChild"
             };
}

// Or setup by this before serialization
[JQPerson mj_setupObjectClassInArray:^NSDictionary *{
        return @{@"childs":@"JQChild"};
    }];

/**************************************************************/

// Define a JSON dictionary
NSDictionary *personDict = @{
                             @"name":@"zjt",
                             @"age":@(31),
                             @"sex":@(JQSexMale),
                             @"address":@"FuZhou",
                             @"marriage":@"true",
                             @"childs":@[@{
                                            @"name":@"zje",
                                            @"age":@(2)
                                            },
                                        @{
                                            @"name":@"zjj",
                                            @"age":@(4)
                                            }]
                             };

// JSON -> Model
JQPerson *person = [JQPerson mj_objectWithKeyValues:personDict];

// Print
for (JQChild *child in person.childs) {
    NSLog(@"childname:%@, childage:%ld\n", child.name, child.age);
}
// childname:zje, childage:2
// childname:zjj, childage:4
```
### JSON array -> model array: `+ mj_objectArrayWithKeyValuesArray`
``` objc
NSArray *dictArray = @[
                         @{
                             @"name" : @"Jack",
                             @"icon" : @"lufy.png"
                         },
                         @{
                             @"name" : @"Rose",
                             @"icon" : @"nami.png"
                         }
                     ];

// JSON array -> User array
NSArray *userArray = [User mj_objectArrayWithKeyValuesArray:dictArray];

// Printing
for (User *user in userArray) {
    NSLog(@"name=%@, icon=%@", user.name, user.icon);
}
// name=Jack, icon=lufy.png
// name=Rose, icon=nami.png
```
### Model array -> JSON array: `+ mj_keyValuesArrayWithObjectArray`
``` objc
// New model array
User *user1 = [[User alloc] init];
user1.name = @"Jack";
user1.icon = @"lufy.png";

User *user2 = [[User alloc] init];
user2.name = @"Rose";
user2.icon = @"nami.png";

NSArray *userArray = @[user1, user2];

// Model array -> JSON array
NSArray *dictArray = [User mj_keyValuesArrayWithObjectArray:userArray];
NSLog(@"%@", dictArray);
/*
 (
 {
 icon = "lufy.png";
 name = Jack;
 },
 {
 icon = "nami.png";
 name = Rose;
 }
 )
 */
```
### Model name - JSON key mapping: `+ mj_replacedKeyFromPropertyName; + mj_setupReplacedKeyFromPropertyName;`
``` objc
// Change the childs array to childname string
@interface JQPerson : NSObject

@property (nonatomic, copy) NSString *name;
@property (nonatomic, assign) NSInteger age;
@property (nonatomic, assign) JQSex sex;
@property (nonatomic, copy) NSString *address;
@property (nonatomic, assign, getter=isMarried) BOOL marriage;
@property (nonatomic, copy) NSString *childname;

@end

// JQPerson.m implements +mj_replacedKeyFromPropertyName method to tell MJExtension how to map
+ (NSDictionary *)mj_replacedKeyFromPropertyName {
    return @{@"childname":@"child.name"};
}

// Or setup by this before serialization
[JQPerson mj_setupReplacedKeyFromPropertyName:^NSDictionary *{
        return @{@"childname":@"child.name"};
    }];

/**************************************************************/

// Define a JSON dictionary
NSDictionary *personDict = @{
                                 @"name":@"zjt",
                                 @"age":@(31),
                                 @"sex":@(JQSexMale),
                                 @"address":@"FuZhou",
                                 @"marriage":@"true",
                                 @"child":@{
                                         @"name":@"zje",
                                         @"age":@(2)
                                         }
                                 };

// JSON -> JQPerson
JQPerson *person = [JQPerson mj_objectWithKeyValues:personDict];   

// Print 
NSLog(@"childname:%@", person.childname);
// childname:zje

```
### NSCoding: `MJExtensionCodingImplementation, + mj_setupIgnoredCodingPropertyNames:;`
``` objc
#import "MJExtension.h"

@implementation Bag
// NSCoding Implementation
MJExtensionCodingImplementation
@end

/***********************************************/

// what properties not to be coded
[Bag mj_setupIgnoredCodingPropertyNames:^NSArray *{
    return @[@"name"];
}];
// Equals: Bag.m implements +mj_ignoredCodingPropertyNames method.

// Create model
Bag *bag = [[Bag alloc] init];
bag.name = @"Red bag";
bag.price = 200.8;

NSString *file = [NSHomeDirectory() stringByAppendingPathComponent:@"Desktop/bag.data"];
// Encoding
[NSKeyedArchiver archiveRootObject:bag toFile:file];

// Decoding
Bag *decodedBag = [NSKeyedUnarchiver unarchiveObjectWithFile:file];
NSLog(@"name=%@, price=%f", decodedBag.name, decodedBag.price);
// name=(null), price=200.800000
```
### NSString -> NSDate, nil -> @"": `- mj_newValueFromOldValue:property:`
``` objc
// Book
#import "MJExtension.h"

@implementation Book
- (id)mj_newValueFromOldValue:(id)oldValue property:(MJProperty *)property
{
    if ([property.name isEqualToString:@"publisher"]) {
        if (oldValue == nil) return @"";
    } else if (property.type.typeClass == [NSDate class]) {
        NSDateFormatter *fmt = [[NSDateFormatter alloc] init];
        fmt.dateFormat = @"yyyy-MM-dd";
        return [fmt dateFromString:oldValue];
    }

    return oldValue;
}
@end

// NSDictionary
NSDictionary *dict = @{
                       @"name" : @"5分钟突破iOS开发",
                       @"publishedTime" : @"2011-09-10"
                       };
// NSDictionary -> Book
Book *book = [Book mj_objectWithKeyValues:dict];

// printing
NSLog(@"name=%@, publisher=%@, publishedTime=%@", book.name, book.publisher, book.publishedTime);
```

---
[MJExtension](https://github.com/CoderMJLee/MJExtension)