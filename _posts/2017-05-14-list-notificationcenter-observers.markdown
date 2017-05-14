---
title:  "List NotificationCenter Observers"
description: How to detect multiple observers of the same event.
## date: 2017-05-14
---

If you want to find out which observers are currently registered in `NotificationCenter`, break and print its debug description:

``` bash
✅(lldb) e print(NotificationCenter.default.debugDescription)
<NSNotificationCenter:0x6000000dc540>
Name, Object, Observer, Options
com.apple.accessibility.SpeakThisEnabled, 0x11088e490, 0x7fcebcc00f10, 1001
com.apple.accessibility.text.legibility.status, 0x11088e490, 0x7fcebcc00f10, 1001
com.apple.accessibility.text.legibility.status, 0x11088e490, 0x608000024220, 1400
UITextEffectsWindowDidRotateNotification, 0x11088e490, 0x7fcebce071a0, 1400
com.apple.accessibility.reduce.motion.status, 0x11088e490, 0x7fcebcc00f10, 1001
UIWindowDidBecomeHiddenNotification, 0x11088e490, 0x60800017be40, 1400
UIDeviceOrientationDidChangeNotification, 0x11088e490, 0x7fcebcc06c20, 1400
… etc.
```
As we can see from the column headers, each row contains `Name`, `Object`, `Observer`, `Options`.
Multiple calls to `NotificationCenter.default.addObserver` with some `NSNotification.Name` will result in multiple entries in this list—_useful to check if a observer hasn't been added too often!_

***

My solution is based on [useyourloaf's "bonus tip"][useyourloaf], that he found in  Foundation Release Notes for OS X v10.11 and iOS 9. 

However, when trying his tip in Xcode 8.3.2 (8E2002) on a Swift 3 code base aimed at iOS Deployment Target 8.0, we  
• (per default) get a truncated list of the observers, so we need to increase the `target.max-string-summary-length`, but also  
• don't get line-breaks in the console output, so it's harder to read. 

…as we can see from the following example:

```
(lldb) p NotificationCenter.default.debugDescription
(String) $R0 = "<NSNotificationCenter:0x6080000caa30>\nName, Object, Observer, Options\ncom.apple.accessibility.SpeakThisEnabled, 0x10f6b0490, 0x7f92a9e01240, 1001\ncom.apple.accessibility.text.legibility.status, 0x10f6b0490, 0x7f92a9e01240, 1001\ncom.apple.accessibility.text.legibility.status, 0x10f6b0490, 0x600000035e00, 1400\nUITextEffectsWindowDidRotateNotification, 0x10f6b0490, 0x7f92a9f0bea0, 1400\ncom.apple.accessibility.reduce.motion.status, 0x10f6b0490, 0x7f92a9e01240, 1001\nUIWindowDidBecomeHiddenNotification, 0x10f6b0490, 0x6080001774c0, 1400\nUIDeviceOrientationDidChangeNotification, 0x10f6b0490, 0x7f92a9f0e020, 1400\nPBDefaultCoercionRegistryDidInstantiateNotification, 0x10f6b0490, 0x60800005d370, 1400\n_UIApplicationForcedUserInterfaceLayoutDirectionChangedNotification, 0x10f6b0490, 0x7f92a9f01960, 1400\n_UIApplicationForcedUserInterfaceLayoutDirectionChangedNotification, 0x10f6b0490, 0x7f92a9f01470, 1400\nUITextInputCurrentInputModeDidChangeNotification, 0x10f6b0490, 0x7f92a9f0bea0, 1400\ncom.apple.accessibility.monoaudio."...
(lldb) set set target.max-string-summary-length 50000
(lldb) p NotificationCenter.default.debugDescription
(String) $R1 = <this time the entire list>
```

Fortunately, I previously found a solution to the [line formatting of an Alamofire debugDescription in Xcode console]({% post_url 2016-11-14-alamofire-debugDescription-on-breakpoint %}) that I could apply here as well.


[useyourloaf]: https://useyourloaf.com/blog/unregistering-nsnotificationcenter-observers-in-ios-9/