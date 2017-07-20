---
title: NJKWebViewProgress 的使用
date: 2016-08-30 13:13:45
categories: 
- Technology
- Programming
- Objective-C
tags: 
- NJKWebViewProgress
---
### 安装
``` bash
pod 'NJKWebViewProgress'
```
<!-- more -->

---

### 使用
#### 导包并遵循协议
``` objc
#import "ViewController.h"
#import "NJKWebViewProgress.h"
#import "NJKWebViewProgressView.h"

@interface ViewController ()<NJKWebViewProgressDelegate>
@property (weak, nonatomic) IBOutlet UIWebView *pageLoadedWV;               /**< 显示加载页面的 WebView */
@property (weak, nonatomic) IBOutlet NJKWebViewProgressView *pageLoadPV;    /**< 显示加载进度的 ProgressView */
@property (nonatomic, strong) NJKWebViewProgress *progressProxy;            /**< 处理加载进度代理 */

@end

```

#### 设置代理并加载界面
``` objc
- (void)viewDidLoad {
    [super viewDidLoad];
    // 设置代理
    self.pageLoadedWV.delegate = self.progressProxy;
    self.progressProxy.progressDelegate = self;
    
    // 通过请求加载页面
    [self.pageLoadedWV loadRequest:[NSURLRequest requestWithURL:[NSURL URLWithString:@"http://coder-zjq.me"]]];
}
```

#### 更新加载进度 
##### 通过代理
``` objc
#pragma mark <NJKWebViewProgressDelegate>
/**
 *  更新加载进度
 *
 *  @param webViewProgress NJKWebViewProgress 对象
 *  @param progress        当前加载进度
 */
- (void)webViewProgress:(NJKWebViewProgress *)webViewProgress updateProgress:(float)progress {
    self.pageLoadPV.hidden = (progress == 1.0);
    [self.pageLoadPV setProgress:progress animated:YES];
}

```

##### 通过 block 回调
``` objc
__weak typeof(self) weakSelf = self;
self.progressProxy.progressBlock = ^(float progress) {
    weakSelf.pageLoadPV.hidden = (progress == 1.0);
    [weakSelf.pageLoadPV setProgress:progress animated:YES];
};
```

---

### 效果
![效果](http://ww2.sinaimg.cn/large/801b780agw1f7bs74x4ltj208w0get9f.jpg)
