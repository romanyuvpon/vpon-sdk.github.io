---
layout: "ios"
title: "iOS - 进阶设定"
lead: "帮助您取得更多广告功能与资料收集"
description:
keywords: 'Keywords for this page, in the meta data'
permalink: /zh-cn/ios/advanced/
lang: "zh-cn"
---
# 自定参数
---
您可以在固定需要新增的 function(getTestIdentifiers) 中设定测试手机的识别码 (在第一次发出 request 时会提示开发者要新增什麽识别码)，让 Vpon 以更精确的方式指定广告。 在开发期间 建议将自己的手机识别码加在 getTestIdentifiers 函式中以免产生不实曝光，造成您收益上的损失，并请在上架前将识别码删除，否则之后填入识别码的手机将无法抓到正常广告

## 增加测试手机的识别码
您可以使用这些属性来指定要接收测试广告的装置或装置 Set。若要确认 SDK 是否已顺利整合，请加入您的测试装置并执行应用程式，然后按一下所显示的测试广告。

```objc
  // 请新增此function到您的程式内 如果为测试用 则在下方填入识别码
  -(NSArray*)getTestIdentifiers
  {
      return [NSArray arrayWithObjects:
              // add your test Id
              @"XXXXXXXXXXXXXXXXXXXXX",
              nil];
  }
```

## 指定目标
您也可以指定位置和客层相关资讯。不过，为了保护使用者隐私，请只指定您的应用程式中现有的位置和客层资料。

   [vpadnAd setUserInfoAge:25];

   [vpadnAd setUserInfoKeyword:@"Game,RPG"];

   [vpadnAd setUserInfoGender:female];

   [vpadnAd setUserInfoBirthdayWithYear:1988 Month:6 andDay:9];


# Protocol
---
您可以在 ViewController 宣告时加入 VpadnBannerDelegate || VpadnInterstitialDelegate 此两个 protocol，藉此追踪请求失败或「点击」等广告事件。



```objc
#pragma mark VpadnBannerDelegate Banner Ad protocol
@protocol VpadnBannerDelegate <NSObject>
@optional

#pragma mark 通知拉取广告成功 pre-fetch 完成
- (void)onVpadnAdReceived:(UIView *)bannerView;

#pragma mark 通知拉取广告失败
- (void)onVpadnAdFailed:(UIView *)bannerView didFailToReceiveAdWithError:(NSError *)error; // alan todo code need to add

#pragma mark 通知开启 vpadn 广告页面
- (void)onVpadnPresent:(UIView *)bannerView;

#pragma mark 通知关闭vpadn广告页面
- (void)onVpadnDismiss:(UIView *)bannerView;

#pragma mark 通知离开 publisher application
- (void)onVpadnLeaveApplication:(UIView *)bannerView;
@end
```

```objc
#pragma mark VpadnInterstitialDelegate Interstitial Ad protocol
@protocol VpadnInterstitialDelegate <VpadnBannerDelegate>
@optional

#pragma mark 通知取得插屏广告成功pre-fetch完成
- (void)onVpadnInterstitialAdReceived:(UIView *)bannerView;

#pragma mark 通知取得插屏广告失败
- (void)onVpadnInterstitialAdFailed:(UIView *)bannerView;

#pragma mark 通知关闭vpadn广告页面
- (void)onVpadnInterstitialAdDismiss:(UIView *)bannerView;
@end
```

这些方法可用于个别的物件，例如

```objc
  #import "VpadnBanner.h"
  #import "VpadnInterstitial.h"
  @interface ViewController : UIViewController<VpadnBannerDelegate, VpadnInterstitialDelegate>
```

将要接收的物件传给 VpadnBanner：

```objc
vpadnAd.delegate = self;
```
当 VpadnBanner 广告抓取成功时传送。

```objc
  - (void)onVpadnAdReceived:(UIView *)bannerView{}
```
当 VpadnBanner 失败时传送；失败原因通常是网路连线失败、应用程式设定错误或广告空间不足。建议您将这些事件记录下来以便侦错：

```objc
  - (void)onVpadnAdFailed:(UIView *)bannerView didFailToReceiveAdWithError:(NSError *)error{}
```

当广告因获得使用者点击，在您的应用程式之前webView 并呈现出全萤幕广告使用者介面时呼叫。

```objc
  - (void)onVpadnPresent:(UIView *)bannerView{}
```
当使用者关闭与 onVpadnDismiss 一同显示的webView，控制权也交还给应用程式时呼叫。

```objc
  - (void)onVpadnDismiss:(UIView *)bannerView;
```
当 Ad 点击会启动新的应用程式(out app)时呼叫。

```objc
  - (void)onVpadnLeaveApplication:(UIView *)bannerView{}
```


# Crazy Ad
---
Crazy Ad 是由 Banner 自动展示的全萤幕富媒体广告，展开后呈现约 5~7 秒会自动关闭。

<img src="{{site.imgurl}}/Crazyad.png" alt="" class="width-300" />


## 如何设定 Crazy Ad
---

1. 请先[注册帐号]成为 Vpon 开发商伙伴
2. 登入[开发商后台]申请 License Key
3. 选择是否播放 Crazy Ad

如图：
![CrazyadSetting]


# Corona User
---
如果您的 App 使用 Corona 欲串接 Vpon 广告，我们建议您用 Web SDK 的方式串接，使用方法如下：

1. 请参考 [Vpon Web SDK 串接说明]，准备一个包含 Web SDK 广告请求的 HTML 档案
2. 在 WebView 中读取该 HTML 档案，例如：webView:request(“localfile.html”, system.ResourceDirectory)

> **Note**：更多 Corona SDK 文件可参考: [Corona Document]

[CrazyadSetting]: {{site.imgurl}}/CrazyadSetting.png
[注册帐号]: {{ site.baseurl }}/zh-cn/ios/registration/
[开发商后台]: http://console.vpon.com
[Vpon Web SDK 串接说明]: {{site.baseurl}}/zh-cn/web/
[Corona Document]: http://docs.coronalabs.com/api/library/native/newWebView.html