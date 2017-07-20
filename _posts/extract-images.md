---
title: 如何抽取其它应用素材 - iOS
date: 2016-04-17 22:01:04
categories: 
- Technology
- Tips
- Other
tags: 
- Extract Images
---
### 准备工作   
#### 下载 ipa ：  
> iTunes --> App Store --> 下载所需素材的应用。下载完成后，可在我的 iPhone 应用 --> 在 Finder 中显示，看到下载的 ipa 文件。   

![ipa文件.png](http://ww3.sinaimg.cn/large/801b780agw1f6yowx86sxj204d06ct8s.jpg)

<!-- more -->

#### 生成 cartool 可执行文件    
> 在 github 上下载 [cartool](https://github.com/steventroughtonsmith/cartool) ，用 Xcode 打开并执行，便可在项目的 Products 文件夹下找到生成 cartool 可执行文件。

`（TIPS：若是需将 cartoon 移动至其他文件夹，不要直接在工程目录下直接拖动，这样只是生成个替身。正确的方式应 show in finder 在 finder 中操作。）`   
![cartool.png](http://ww3.sinaimg.cn/large/801b780agw1f6yoyp3r0kj205f050weo.jpg)  

---

### 具体步骤 
#### 右击下载的 ipa 文件 --> 打开方式 --> 选择归档实用工具；   
![归档实用工具.png](http://ww1.sinaimg.cn/large/801b780agw1f6yozw2lrqj205s03k3yo.jpg)
#### 可解档出一文件夹 --> Payload --> 显示包内容；  
![显示包内容.png](http://ww3.sinaimg.cn/large/801b780agw1f6yp0d753tj20cn02a74j.jpg)
#### 在该包内便有部分所需的素材；   
![包内容.png](http://ww2.sinaimg.cn/large/801b780agw1f6yp18adylj205e06pdgl.jpg)
#### 但还有部分素材保存在 Assets.car 文件中，此时就可以用到刚才生成的 cartool ，抽取其中的素材；  
![Assets_car.png](http://ww4.sinaimg.cn/large/801b780agw1f6yp1sftbbj2048064zka.jpg)
#### 打开终端 cd 到 cartool 所在的文件夹下，执行命令 `./cartool [Assets.car所在文件夹] [存放素材的文件夹]` ，便可获得 Assets.car 中的素材。     
![cd_cartool.jpg](http://ww2.sinaimg.cn/large/801b780agw1f6yp2dca7xj20bl01mmxf.jpg) 

![素材.png](http://ww2.sinaimg.cn/large/801b780agw1f6yp2u7i8jj205g07jmy1.jpg)
#### 获取的素材一般会带有 "~iphone" 或者 "~ipad" ，使用时需替换掉，因此需批量更改素材名，可用 Xcode 编写代码

``` objc
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        
        //  素材文件夹路径（输入自己的）
        NSString *filePath = @"/Users/Joker/....../Images";
        
        //  获取文件管理者
        NSFileManager *manager = [NSFileManager defaultManager];
        
        //  获取该文件夹下所有文件名
        NSArray *fileNames = [manager contentsOfDirectoryAtPath:filePath error:nil];
        
        //  遍历文件名
        for (NSString *fileName in fileNames) {
            
            //  为修改前的文件路径
            NSString *fromPath = [filePath stringByAppendingPathComponent:fileName];
            
            //  将“~iphone”替换为“”，最好用正则表达式，此处仅简单替换
            NSString *changeToName = [fileName stringByReplacingOccurrencesOfString:@"~iphone" withString:@""];
            
            //  拼接该玩的文件名至路径
            NSString *toPath = [filePath stringByAppendingPathComponent:changeToName];
            
            //  将素材移动至修改完的路径
            [manager moveItemAtPath:fromPath toPath:toPath error:nil];
            
        }
    }
    return 0;
}

```

---
### 利用插件
有个大神写了个插件 `iOS Images Extractor` ，就是下面这个：   
![iOS Images Extractor.png](http://ww4.sinaimg.cn/large/801b780agw1f6yp3j4sjaj203s03djrg.jpg)

不过好像删除了，如果有需要的话下面是分享的下载地址。使用的话直接将 ipa 文件拖进去就可以。   

![插件界面](http://ww1.sinaimg.cn/large/801b780agw1f6yp3x2y04j20go0cat9b.jpg)

[项目地址](https://github.com/duiyueliu/iOS-Images-Extractor-master)   
[插件地址](https://pan.baidu.com/s/1dFNrF4P)


*（注意，抽取的素材仅供学习，不要用于其他商业用途）*
