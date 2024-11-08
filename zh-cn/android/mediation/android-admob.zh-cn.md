---
layout:         "android"
title:          "Android - Admob 使用串接"
lead:           ""
description:    ""
keywords:       "Keywords for this page, in the meta data"
permalink:       zh-cn/android/mediation/admob/
lang:           "zh-cn"
---
# 概要
---
以下为搭配 Google AdMob 进行广告串接的设定方式。在开始进行设定之前，请先参考[串接说明]将 Vpon SDK 加到您的专案中。请注意，要使用 Google AdMob 进行广告串接的话，请务必确认您的专案中包含以下三个档案：

1. Google Mobile Ads SDK
2. Vpon SDK
3. Vpon AdMob Adapter

>**Note:** 
>
>* 除了实作广告串接的部份外，为使广告正常运作，并在适当的时机释放资源，我们建议可以在 Activity 生命中期中呼叫对应的方法 (请参考 [Google Ads API])
>
>* 您可以[由此下载][2] Vpon SDK 及 Vpon AdMob Adapter。


# 广告单元设定
---

## 新增应用程式
首先，请登入您的 [AdMob][1] 后台，根据应用程式平台来新增应用程式，并取得应用程式 ID

<img src="{{site.imgurl}}/AdMob_012.png" alt="" class=""/>

## 新增广告单元
新增应用程式后，请选择要新增的广告单元格式，并取得广告单元 ID
<img src="{{site.imgurl}}/AdMob_013.png" alt="" class=""/>

请将应用程式 ID 及广告单元 ID 加到您的应用程式专案中，以取得广告

# 中介服务设定
---

## 中介服务群组
切换到中介服务标签，选择创建中介组
<img src="{{site.imgurl}}/AdMob_014.png" alt="" class=""/>

根据您的应用程式平台及广告格式建立中介组
<img src="{{site.imgurl}}/AdMob_015.png" alt="" class=""/>

选择要加入的广告单元
<img src="{{site.imgurl}}/AdMob_016.png" alt="" class=""/>
<img src="{{site.imgurl}}/AdMob_017.png" alt="" class=""/>

## 广告联盟设定
如果您要串接的是横幅广告或插页广告，请选择添加广告联盟將 Vpon 新增为您的广告联盟
<img src="{{site.imgurl}}/AdMob_018.png" alt="" class=""/>

选择 Vpon
<img src="{{site.imgurl}}/AdMob_019.png" alt="" class=""/>

请在 Vpon Ad ID 的栏位中，填入您申请的 Vpon License Key，并在 Zone 的栏位中，填入 "TW"
<img src="{{site.imgurl}}/AdMob_020.png" alt="" class=""/>


## 自定义事件设定 {#customevent}
如果您要串接的是原生广告，请选择添加自定义事件將 Vpon 新增为您的广告联盟
<img src="{{site.imgurl}}/AdMob_021.png" alt="" class=""/>

请在 Class Name 的栏位中，填入 CustomEvent 的 Class Name，例：Android 為 `com.vpadn.mediation.VpadnAdapter`，并在 Parameter 中填入您申请的 Vpon License Key
<img src="{{site.imgurl}}/AdMob_022.png" alt="" class=""/>


>**Note**: 使用 AdMob Mediation 搭配 Vpon Adapter 串接原生广告时，adListener 的行为可能会与单独使用 AdMob 不一致。<br>
可能会受到影响的 adListener: `onAdLeftApplication`、`onAdClosed`


# Tips
---

### Sample Code
如果您想看到完整的串接实例，请参考我们的 [Sample Code]


[串接说明]:http://wiki.vpon.com/zh-cn/android/integration-guide/
[1]:https://apps.admob.com
[Sample Code]: {{site.baseurl}}/zh-cn/android/download
[2]: {{site.baseurl}}/zh-tw/android/download
[Google Ads API]: https://developers.google.com/android/reference/com/google/android/gms/ads/BaseAdView#pause()