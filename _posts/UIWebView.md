---
title: UIWebView 的简单使用
date: 2016-08-30 15:17:55
categories: 
- Technology
- Programming
- Objective-C
tags: 
- UIWebView
---
### 简介
> 你可以在你的 APP 中使用 UIWebView 内嵌网页内容，你也可以在网页浏览历史中前进或后退，甚至利用代码改变网页内容。除了 HTML 网页以外，UIWebView 还可以用来展示其它内容，例如：Keynote、PDF 以及 Pages 文档，但是为了富文本的更好渲染，还是最好使用 UITextView。

<!-- more -->

---

### 使用
#### 加载页面
``` objc
/**
 *  通过 URL 请求加载页面
 *
 *  @param request URL 请求，其中 URL 可以为加载文件的路径
 */
- (void)loadRequest:(NSURLRequest *)request;
/**
 *  通过载入一段 HTML 字符串加载页面
 *
 *  @param string  HTML 字符串
 *  @param baseURL 基本路径，用于寻找页面中图片等资源
 */
- (void)loadHTMLString:(NSString *)string baseURL:(nullable NSURL *)baseURL;
/**
 *  通过二进制数据加载页面（较少用）
 *
 *  @param data             数据
 *  @param MIMEType         数据类型
 *  @param textEncodingName 数据编码形式
 *  @param baseURL          基本路径，用于寻找页面中图片等资源
 */
- (void)loadData:(NSData *)data MIMEType:(NSString *)MIMEType textEncodingName:(NSString *)textEncodingName baseURL:(NSURL *)baseURL;
```
#### UIWebViewDelegate 代理
``` objc
/**
 *  是否根据请求开始加载页面
 *
 *  @param webView        显示页面的 UIWebView
 *  @param request        加载的请求
 *  @param navigationType 用户行为类型
 *
 *  @return     YES：加载页面
                NO：不加载页面
 */
- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType;
/**
 *  WebView 已经开始加载页面
 *
 *  @param webView 显示页面的 WebView
 */
- (void)webViewDidStartLoad:(UIWebView *)webView;
/**
 *  WebView 已经结束加载页面
 *
 *  @param webView 显示页面的 WebView
 */
- (void)webViewDidFinishLoad:(UIWebView *)webView;
/**
 *  WebView 加载页面失败
 *
 *  @param webView 显示页面的 WebView
 *  @param error   错误信息
 */
- (void)webView:(UIWebView *)webView didFailLoadWithError:(nullable NSError *)error;
```
####相关属性
``` objc
/** UIWebViewDelegate 代理 */
@property (nullable, nonatomic, assign) id <UIWebViewDelegate> delegate;
/** 内嵌的 UIScrollView */
@property (nonatomic, readonly, strong) UIScrollView *scrollView NS_AVAILABLE_IOS(5_0);
/** 载入的请求 */
@property (nullable, nonatomic, readonly, strong) NSURLRequest *request;
/** 当前页面是否可以后退 */
@property (nonatomic, readonly, getter=canGoBack) BOOL canGoBack;
/** 当前界面是否可以前进 */
@property (nonatomic, readonly, getter=canGoForward) BOOL canGoForward;
/** 当前页面是否正在加载 */
@property (nonatomic, readonly, getter=isLoading) BOOL loading;
/** 设置页面是否缩放至屏幕大小 */
@property (nonatomic) BOOL scalesPageToFit;
/** 已弃用 */
@property (nonatomic) BOOL detectsPhoneNumbers NS_DEPRECATED_IOS(2_0, 3_0);
/** 设置可转换成链接的类型 */
@property (nonatomic) UIDataDetectorTypes dataDetectorTypes NS_AVAILABLE_IOS(3_0);
/** 设置是否使用内联播放器播放，iPad 默认为 YES，iPhone 默认为 NO */
@property (nonatomic) BOOL allowsInlineMediaPlayback NS_AVAILABLE_IOS(4_0);
/** 设置播放器自动播放还是需用户点击，iPad 及iPhone 默认均为 YES */
@property (nonatomic) BOOL mediaPlaybackRequiresUserAction NS_AVAILABLE_IOS(4_0); 
/** 设置是否支持 Air Play，iPad 及 iPhone 默认均为 YES */
@property (nonatomic) BOOL mediaPlaybackAllowsAirPlay NS_AVAILABLE_IOS(5_0); 
/** 设置是否将数据加载入内存后渲染界面，iPhone 及 iPad 默认均为 NO */
@property (nonatomic) BOOL suppressesIncrementalRendering NS_AVAILABLE_IOS(6_0); 
/** 是否自动展示键盘，默认为 YES */
@property (nonatomic) BOOL keyboardDisplayRequiresUserAction NS_AVAILABLE_IOS(6_0); 
/** 设置当网页的大小超出view时的分页显示模式 */
@property (nonatomic) UIWebPaginationMode paginationMode NS_AVAILABLE_IOS(7_0);
/** 这个属性决定了CSS属性是采用column-break 还是page-breaking样式 */
@property (nonatomic) UIWebPaginationBreakingMode paginationBreakingMode NS_AVAILABLE_IOS(7_0);
/** 分页长度 */
@property (nonatomic) CGFloat pageLength NS_AVAILABLE_IOS(7_0);
/** 多个页面之间差距值 */
@property (nonatomic) CGFloat gapBetweenPages NS_AVAILABLE_IOS(7_0);
/** 分页个数 */
@property (nonatomic, readonly) NSUInteger pageCount NS_AVAILABLE_IOS(7_0);
/** 设置多媒体播放是否支持画中画 */
@property (nonatomic) BOOL allowsPictureInPictureMediaPlayback NS_AVAILABLE_IOS(9_0);
/** 设置是否支持链接预览 */
@property (nonatomic) BOOL allowsLinkPreview NS_AVAILABLE_IOS(9_0); // default is NO
```
#### 其它方法
``` objc
/**
 *  重新加载页面
 */
- (void)reload;
/**
 *  停止加载页面
 */
- (void)stopLoading;
/**
 *  返回至上一个页面，可以配合 canGoBack 属性使用
 */
- (void)goBack;
/**
 *  前进至刚才的页面，可以配合 canGoForward 属性使用
 */
- (void)goForward;
/**
 *  通过 JavaScript 获取页面字符串，可以通过该方法注入 JavaScript 改变页面
 *
 *  @param script JavaScript 字符串
 *
 *  @return 获得的字符串
 */
- (nullable NSString *)stringByEvaluatingJavaScriptFromString:(NSString *)script;
```

#### 各枚举类型
``` objc
/**
 *  用户触发行为类型
 */
typedef NS_ENUM(NSInteger, UIWebViewNavigationType) {
    UIWebViewNavigationTypeLinkClicked,     //用户触发了一个链接
    UIWebViewNavigationTypeFormSubmitted,   //用户提交了一个表单
    UIWebViewNavigationTypeBackForward,     //用户触击前进前进或返回按钮
    UIWebViewNavigationTypeReload,          //用户触击重新加载的按钮
    UIWebViewNavigationTypeFormResubmitted, //用户重复提交表单
    UIWebViewNavigationTypeOther            //发生了其他行为
};
/**
 *  可转换为链接的类型
 */
typedef NS_OPTIONS(NSUInteger, UIDataDetectorTypes) {
    UIDataDetectorTypePhoneNumber       // 电话号码
    UIDataDetectorTypeLink              // URL 链接
    UIDataDetectorTypeAddress           // 地址
    UIDataDetectorTypeCalendarEvent     // 日程
    UIDataDetectorTypeNone              // 不转换
    UIDataDetectorTypeAll               // 全转换
};
/**
 *  页面分页模式
 */
typedef NS_ENUM(NSInteger, UIWebPaginationMode) {
    UIWebPaginationModeUnpaginated,     //不使用分页效果
    UIWebPaginationModeLeftToRight,     //将网页超出部分分页，从左向右进行翻页
    UIWebPaginationModeTopToBottom,     //将网页超出部分分页，从上向下进行翻页
    UIWebPaginationModeBottomToTop,     //将网页超出部分分页，从下向上进行翻页
    UIWebPaginationModeRightToLeft      //将网页超出部分分页，从右向左进行翻页
};
/**
 *  这个枚举决定了webView加载页面具有CSS属性时是使用页的样式还是以列的样式。
 */
typedef NS_ENUM(NSInteger, UIWebPaginationBreakingMode) {
    UIWebPaginationBreakingModePage,    //默认设置是这个属性，CSS属性以页样式。
    UIWebPaginationBreakingModeColumn   //当UIWebPaginationBreakingMode 设置这个属性的时候，这个页面内容 CSS 属性以 column-break 代替 page-breaking 样式。
};
```
#### 注意
- 不可以将 UIWebView 或者 UITableView 内嵌至 UIScrollView 对象，因为触摸事件会在两个对象间混乱，因而作出错误的操作；
- 如果是运行在 iOS 8 以上的系统可以使用 WKWebView 取代 UIWebView。
---

### 其它
可以结合一下第三方类库使用：   
- [NJKWebViewProgress](https://github.com/ninjinkun/NJKWebViewProgress)：页面加载进度显示；   
- [WebViewJavascriptBridge](https://github.com/marcuswestin/WebViewJavascriptBridge)：用于 Objective-C ↔ JavaScript 之间的交互。