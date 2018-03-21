---
layout:         "ios"
title:          "iOS - 詳細設定"
lead:           ""
description:    ""
keywords:       "Keywords for this page, in the meta data"
permalink:       jp/ios/advanced/
lang:            "jp"
---
# カスタムパラメータ
---
本function(getTestIdentifiers) 内にテストIDを入力し、掲載テストを実施することができます。（最初のリクエスト時にユニークIDの追加を促します）開発中の広告の無駄な露出と収益損失を防ぐため、テスト用端末IDを入力いただくことをおすすめいたします。また、テスト完了後はテスト用広告を掲載しないよう、テスト用端末IDを忘れずに削除してください。

## テスト用端末ID の追加
これらのプロパティでテスト広告を表示させる端末、もしくは端末セットを指定することができます。
開発中に不要な広告を表示させないためにこのプロパティをご利用ください。
SDKが正しく実装されていることを確認するには、テスト用端末を追加し、アプリを起動させ、表示されたテスト広告をクリックします。


```objc
// この機能をプログラム内に追加し、下方にテスト端末IDを記入する
-(NSArray*)getTestIdentifiers
{
    return [NSArray arrayWithObjects:
          // add your test Id
          @"XXXXXXXXXXXXXXXXXXXXX",
          nil];
}
```

## ターゲティング
位置情報とユーザー属性情報を指定することができます。ユーザーのプライバシー情報保護の観点から、アプリ内の既存情報としての位置情報とユーザー属性情報を指定してください。

   [vpadnAd setUserInfoAge:25];

   [vpadnAd setUserInfoKeyword:@"Game,RPG"];

   [vpadnAd setUserInfoGender:female];

   [vpadnAd setUserInfoBirthdayWithYear:1988 Month:6 andDay:9];


# Protocol
---
ViewController の宣言時にこの2つのプロトコルを追加することで、広告リクエストの失敗やクリックスルーなどのライフサイクルイベントをトラッキングすることができます。


```objc
#pragma mark VpadnBannerDelegate  general banner protocol
@protocol VpadnBannerDelegate <NSObject>
@optional
#pragma mark sent when ads has succeeded
- (void)onVpadnAdReceived:(UIView *)bannerView;
#pragma mark sent when ads has failed
- (void)onVpadnAdFailed:(UIView *)bannerView didFailToReceiveAdWithError:(NSError *)error; // alan todo code need to add
#pragma mark sent immediately before the user is presented with Vpadn ad
- (void)onVpadnPresent:(UIView *)bannerView;
#pragma mark sent when the Vpadn ad is dismissed
- (void)onVpadnDismiss:(UIView *)bannerView;
#pragma mark sent just before the application gets backgrounded or terminated
- (void)onVpadnLeaveApplication:(UIView *)bannerView;
@end
```

```objc
#pragma mark VpadnInterstitialDelegate Interstitial Ad protocol
@protocol VpadnInterstitialDelegate <VpadnBannerDelegate>
@optional
#pragma mark sent when interstitial ads has succeeded
- (void)onVpadnInterstitialAdReceived:(UIView *)bannerView;
#pragma mark sent when interstitial ads has failed
- (void)onVpadnInterstitialAdFailed:(UIView *)bannerView;
#pragma mark sent when the Vpadn ad is dismissed
- (void)onVpadnInterstitialAdDismiss:(UIView *)bannerView;
@end
```

これらのメソッドは、ViewController ような個別のオブジェクトに使用できます。

```objc
#import "VpadnBanner.h"
#import "VpadnInterstitial.h"
@interface ViewController : UIViewController<VpadnBannerDelegate, VpadnInterstitialDelegate>
```

受信しようとするオブジェクトを VpadnBanner に渡します。

```objc
vpadnAd.delegate = self;
```
広告の取得に成功した際に受け渡します。

```objc
- (void)onVpadnAdReceived:(UIView *)bannerView{}
```
広告取得失敗の際に渡します。一般的には、ネットワーク・アプリの設定ミス・広告在庫の不足が考えられます。デバッグ用にこれらのイベントを記録しておくことをお奨めします。

```objc
- (void)onVpadnAdFailed:(UIView *)bannerView didFailToReceiveAdWithError:(NSError *)error{}
```

ユーザーが広告をクリックし、アプリ上でフルスクリーン広告のユーザーインターフェースが表示される時に呼び出されます。

```objc
- (void)onVpadnPresent:(UIView *)bannerView{}
```
ユーザーが onPresentScreen と一緒に表示されるフルスクリーンアクティビティを閉じ、制御権がアプリに返された時に呼び出す。

```objc
- (void)onVpadnDismiss:(UIView *)bannerView;
```
新しいアプリケーションを起動したときに広告のクリックを呼び出します。

```objc
- (void)onVpadnLeaveApplication:(UIView *)bannerView{}
```

# Crazy Ad
---
バナーがディスプレイ全体にエキスパンドし、5-7秒後に自動的に閉じます。
<img src="{{site.imgurl}}/Crazyad.png" alt="" class="width-300" />


## Setting
---
管理画面にてCrazy ADを配信するかどうかを選択します。

<http://console.vpon.com/> 台湾エリアのプロパティIDを登録

図:
![CrazyadSetting]



# Corona User
---
App を Corona で Vpon 広告に連結しようとする場合、web SDK の方式で連結するようお勧めま す。使用方法は、以下の通りとします。
web SDK 内の html を local file に書き込んでから webview にこの file を load させます (例: webView:request( "localfile.html", system.ResourceDirectory ))。

html コンテンツは、vpon wiki の web SDK 操作マニュアル: [Web SDK をご覧ください]

詳細な Corona SDK ドキュメントは Corona Document: [をご覧ください]




[CrazyadSetting]: {{site.imgurl}}/CrazyadSetting_JP.png
[Web SDK をご覧ください]: {{site.baseurl}}/jp/web/
[をご覧ください]: http://docs.coronalabs.com/api/library/native/newWebView.html
