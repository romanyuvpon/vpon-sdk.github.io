---
layout:         "android"
title:          "Android - インテグレーションガイド"
lead:           ""
description:    ""
keywords:       "Keywords for this page, in the meta data"
permalink:       jp/android/integration-guide/
lang:            "jp"
---
# Vpon SDK 基本編
----
旧バージョンのSDKをご利用の場合、まず最新版のSDKにバージョンアップするための修正をご確認ください。 [SDK4.5.1+ の最新バージョンへのアップデート方法](../../android/latest-news/update-to-SDK4_5_1+/)

1. まず下記URLから登録済みネットワークプラットフォームを確認してください:<br>
台湾: <http://tw.pub.vpon.com/><br>

2. 台湾のプラットフォームを利用する場合、以下をご利用ください:<br>
`vponBanner = new VpadnBanner(this, bannerId, VpadnAdSize.SMART_BANNER,
“TW”);`


# 概要
--------
Vpon バナー広告は、小さなエリアを利用し、ユーザーにクリックさせることで、ウェブサイトもしくはアプリのダウンロードページなどの情報豊富なフルスクリーンページへ遷移させます。ここではあなたのアプリへバナー広告を配信する方法をご案内します。

Android アプリでバナー広告を表示させるためには、Eclipse プロジェクトにSDKを導入し、ユーザインターフ ェースに com.vpadn.ads.VpadnBanner を追加するだけです。

# SDK の導入
----------

Vpon provides two ways to integrate our SDK. Choose one of the following two options:

* [Streamlined Simple? , using Maven,](#maven)<br>
* [Manual, using the SDK download.](#manual-sdk)<br>
<br>

## Streamlined, using Maven {#maven}

Follow the description below and add the link of the Maven repository in `allprojects` in the project-level `build.gradle`.

```javascript
allprojects {
    repositories {
        jcenter()
        maven{
            url 'https://dl.bintray.com/vpon-sdk/maven'
        }
    }
}
```

Add the compile dependency with the assigned version of the Vpon SDK in the app-level `build.gradle` (Here take SDK 4.6.0 for example).

```javascript
dependencies {
    ...
    compile 'com.vpon:vpadnSDK:4.6.0'
}
```

> Publisher can revise the above-mentioned to ``'com.vpon:vpadnSDK:4.6.+'`` to gain the latest SDK in version 4.6.

<br>

## Manual, using the SDK download {#manual-sdk}

アプリにVpon広告を導入するためには、次の3つのステップを完了させてください。

1.  Android Studio/Eclipse プロジェクトに Vpon SDK JAR を追加します。
2.  AndroidManifest.xml で com.vpadn.widget.VpadnActivity を宣言 します。
3.  情報マニフェストで必要な permissions を設定します。

### Eclipse
---
1. Eclipse 内のアプリプロジェクト上でマウスの右ボタンをクリックし、[プロパティ]を選びます。
<img src = "{{site.imgurl}}/A-sdk330-01.png" alt="elcipse-img1" class="width-400">

2. [Java Build Path] (Java 構築パス)と[Libraries] (ライブラリ)のタブを選択してから[Add External JARs...] (外部 JAR...を追 加)をクリックして、Vpon 広告の JAR を追加します。
![]({{site.imgurl}}/A-sdk330-02.png)
<br>


### Android Studio
---
1. Find `libs` in your Android project (Route：Project Name -&gt; app
-&gt; Android プロジェクトの「libs」を選んでください。(ルート:プロジェクト名 -&gt; app -&gt; libs)
![]({{site.imgurl}}/ProjectLibFolder.jpg)


2. `libs` の所で右クリックをし、`Reveal in Finder` を選び左クリックしてください。
![]({{site.imgurl}}/DropJarFileToLibFolder.jpg)


3. ダウンロードした JAR を Finder にある `libs` に移動させてください。(IDE で `libs` に Vpon JAR をドラッグして入れることも可能です)
![]({{site.imgurl}}/MainInterface.jpg)



4. Android プロジェクトに戻り、先ほど追加した Vpon JAR が `libs` に表示されていること を確認してください。参考リンク先をリンクさせるには、右クリックし、ライブラリとし て追加を選択してください。同時に、「コンパイルファイル ('libs/vpon_SDK_version_name.jar')」という文章があるか、 build.gradle を確認してくださ い。下の写真をご参考ください
![]({{site.imgurl}}/ModifyBuildGradle.jpg)

# VpadnActivity
---
以下の設定を AndroidManifest.xml に追加します。

```xml
<activity
  android:name="com.vpadn.widget.VpadnActivity"
  android:configChanges="orientation|keyboardHidden|navigation|keyboard|screenLayout|uiMode|screenSize|smallestScreenSize"
  android:theme="@android:style/Theme.Translucent"
  android:hardwareAccelerated="true" >
</activity>
```

> **Note**: 上記の各属性はいずれも必須で、その値は全て同じとなります。

<br>

# パーミション
---
以下のパーミッションを AndroidManifest.xml に追加します。

```java
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
   <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
```

上記3つは 必須パーミッションとなります。さらに、下記のパーミッションを追加することで、より正確にエリアターゲティング広告を取得いただくことをお奨めいたします。

```java
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
  <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```

ビデオ広告をサポートするために、アクティビティにてハードウェアアクセラレータを有効にしていただくことをお奨めいたします。

```xml
<activity
  android:name="com.vpadn.example.MainActivity"
  android:label="@string/app_name"
  android:configChanges="keyboardHidden|orientation"
  android:hardwareAccelerated="true" >
  <intent-filter>
    <action android:name="android.intent.action.MAIN" />
    <category android:name="android.intent.category.LAUNCHER" />
  </intent-filter>
</activity>
```
  []: A-skd330-01.png "fig:A-skd330-01.png"
  [1]: A-sdk330-02.png "fig:A-sdk330-02.png"


# サンプルコードのダウンロード
---
[Go to download page](../download)

# ヒント
---

より詳細な情報は、[バナー広告](../banner)、[ンタースティシャル広告](../interstitial)、[メディエーション](../mediation)をご確認 ください。
