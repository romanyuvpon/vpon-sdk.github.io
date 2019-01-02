---
layout:         "ios"
title:          "iOS - DMP SDK"
lead:           ""
description:    "dmp"
keywords:       ""
permalink:       ios/dmp/
lang:            "en"
---

# Prerequisites
---

### System requirement
Deployment target 7.0 above.

### Import SDK
You can [download Vpon DMP SDK here](http://m.vpadn.com/sdk/vpadn-dmp-iOS-1.1.0-a41ba9f.tar.gz). A Objective-c Header file and a lib file will included. Please follow the steps below to integrate Vpon DMP SDK to your Xcode project.

1. Add `VpadnAnalytics.h`, `VATracker.h` and `VpadnDictionaryBuilder.h` to your project.
2. Add `AdSupport.framework` to your project.

# Start To Implement Vpon DMP SDK
---
Please follow the steps below to integrate Vpon DMP SDK in your application.

### Import Vpon DMP SDK

Please import VpadnAnalytics.h in every page that will integrate with Vpon Analytics.

```objc
#import "VpadnAnalytics.h";
```

### Declare VpadnAnalytics and Indicate A License Key

Please follow the sample code below to indicate a License Key when you call VpadnAnalytics sharedInstance for the first time.

```objc
[[VpadnAnalytics sharedInstance] setLicenseKey:@"License Key"];
```

> **Note:** Please replace the License Key with your own one.

### Send Message
Vpon DMP SDK provide two methods to send messages as below:

#### sendLaunchEvent()
sendLaunchEvent() can be used when user launch the App. We recommend that you can add this method in didFinishLaunchingWithOptions of AppDelegate.

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions{
    [[VpadnAnalytics sharedInstance] setLicenseKey:@""];
    [[VpadnAnalytics sharedInstance].defaultTracker sendLaunchEvent:@"customID"];
    return YES;
}
```

#### send()
send() can be used to send message in most of events. You can send message with or without payload.

* send message without payload：

```objc
[[VpadnAnalytics sharedInstance].defaultTracker send:[[VpadnDictionaryBuilder createEventWithEventType: Event_Custom customID:nil extraData:nil]build]];
```

* send message with payload：

```objc
NSMutableDictionary* dicExtraData = [[NSMutableDictionary alloc]initWithCapacity:1];
    [dicExtraData setObject:@"just for test" forKey:@"testInfo"];
    NSDictionary* dicJSONData = [[NSDictionary alloc]initWithObjectsAndKeys:@"VponInc", @"facebook", @"testValue", @"custom",nil];
    [dicExtraData setObject:dicJSONData forKey:@"member_id"];
    [[VpadnAnalytics sharedInstance].defaultTracker send:[[VpadnDictionaryBuilder createEventWithEventType:Event_Login customID:@"testKey" extraData:dicExtraData]build]];
    dicJSONData = nil;
    dicExtraData = nil;
```

* You can also call send() as below if you want to send message with specific event (all events are available):

```objc
[[VpadnAnalytics sharedInstance].defaultTracker send:[[VpadnDictionaryBuilder createEventWithEventName:@"testEvent" customID:nil extraData:nil]build]];
```

> **Note:**
>
> 1. Please refer to the EventType of VpadnDictionaryBuilder to implement the parameter of createEventWithName.
> 2. If you want to print debug log in console section, please add a parameter in Building Setting. The key should be SHOW_VPON_LOG, the value should be "1".



# Download
---

|DMP 1.1.0|
|:-------:|
|[Download](http://m.vpadn.com/sdk/vpadn-dmp-iOS-1.1.0-a41ba9f.tar.gz)|