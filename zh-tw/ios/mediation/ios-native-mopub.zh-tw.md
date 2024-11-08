---
layout:         "ios"
title:          "iOS (原生廣告) 中介服務 - MoPub"
lead:           ""
description:    ""
keywords:       "Keywords for this page, in the meta data"
permalink:       /zh-tw/ios/native/mediation/mopub/
lang:           "zh-tw"
---

# 概要
---
在開始進行 MoPub 設定之前，請務必確認您的專案中已包含以下三個檔案：

1. MoPub SDK
2. Vpon SDK
3. Vpon MoPub Custom Events

並參考[串接說明]初始化 Vpon iOS SDK。

>**Note:** 您可以[由此下載][13] Vpon SDK 及 Vpon MoPub Custom Events。

# MoPub 設定
---
Mopub 後台設定請參考下列步驟:

## Step1: 新增 app
選擇 Inventory 選項並點擊 "Add a New App" 新增您的 app。
![][6]

## Step2: 新增廣告
進入剛註冊的 app 後點選 "Add an Ad Unit" 並選擇要新增的廣告類型。
![][10]

## Step3: 新增 Vpon Ad Network
選擇 "Networks" 選項並點擊 "add a Network"。
![][1]

## Step4: Custom Native Network
選擇 Custom Native Network
![][2]

## Step5: 填入標題名稱
填入辨識用的標題名稱, 方便您管理增加的 Ad network
![][3]

## Step6: 填寫 CUSTOMEVENT
填入您的 package name + class name, 可以參考範例所示

## Step7: License Key / adUnitID
填入您的 License Key, key 為 `strBannerId`
![][11]

## Step8: 開啟授權 Vpon Ad Network
選擇 "Segments" 選項並選擇 "Global Segment"，可以看到剛建立的 app、廣告、Vpon ad network。請開啟對 Vpon Ad Network 的授權，並確認狀態為 "Running"。

![][12]

# Download
---
[點此處下載Sample Code]。


  [1]: {{site.imgurl}}/Mopub_001.png
  [2]: {{site.imgurl}}/Mopub_002.png
  [3]: {{site.imgurl}}/Mopub_003.png
  [4]: {{site.imgurl}}/Mopub_004-a.png
  [5]: {{site.imgurl}}/Mopub_005.png
  [6]: {{site.imgurl}}/Mopub_006.png
  [10]: {{site.imgurl}}/Mopub_010.png
  [11]: {{site.imgurl}}/Mopub_011.png
  [12]: {{site.imgurl}}/Mopub_012.png
  [點此處下載Sample Code]: {{site.dnldurl}}/sample-code/iOSMoPubNativeMediationSample.zip
[串接說明]: ../../integration-guide/#initial-sdk

[13]: {{site.baseurl}}/zh-tw/ios/download