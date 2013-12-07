--- 
layout: post
title: "iPhone App : Debug and Release through Titanium"
comments: true
categories: 
- app store
- certificates
- distribution
- iPhone app
- iPhone/iPad
- provisioning profile
- release
- Titanium
- titanium app
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: iphone-app-debug-and-release-through-titanium
  aktt_notify_twitter: "no"
---
Once people develop an iPhone App using <a href="http://www.appcelerator.com/">Titanium1.4</a>, they must be very happy when the App is running on iPhone simulator. They feel great until they decide to debug their app on their devices or even release their app to AppleAppStore. This happens specially to these who firstly do this. Why? There are many reasons that you will hate Apple during the debug or release process. I bat you are like me then.

Assume that: You've already finished coding an iPhone app in Titanium 1.4 framework. Now you want to install your app on your device. If you do this first time, guess what will happen to you? Let me tell you my story.

You will be blocked by Titanium certificates detections when you want to install your app to your device. see below image:
<div class="thumbnail"><a href="http://skitch.com/yorzi/dut81/mail-1320x770"><img src="http://img.skitch.com/20100825-fuf9q1dac5ir21f5g4im2h93gi.jpg" alt="mail (1320շ70)" /></a><br /></div>
<br />
Well, in order to become an iPhone developer, you should pay Apple for an iPhone Program Permission. My boss paid Apple for an iPhone Program Team permission, it cost him about one month to pass Apple's approval. After that, he, as an admin agent iPhone developer, invited me as an iPhone developer member with admin permission. Here we had been running into issue for two days. Finally, we found that he only can invite my exist Apple ID as an iPhone developer, because I can't finish a registration process after he invite me with a non-exist Apple ID. The evil is Apple indicates that, we should invite non-exist accounts as team members.

Now have I got the permission to debug my app on my iphone? Wait a moment. Actually I should be invited twice separately, one is for <a href="https://itunesconnect.apple.com/">iTunesconnect</a>. another one is for <a href="http://developer.apple.com/iphone/index.action">Provisioning Portal</a>(Dev Center). These two sites are different, only in Dev Center, I can config my provisioning profile, which is a main concept for releasing iPhone App or allowing to install App on certain devices. But in iTunesconnect, I need to release my app to iTunes/Apple App Store.

So far, I've got enough permission to debug the App on my own iPhone. But I am still unable to distribute my App to others' devices. How that happens? As an iPhone developer, I need to pass Titanium's detection of several certificates. only after that, I can install app on my iPhone. (PS: if you want to test your app on Android, the only need is to connect your device.)

In following images, I will show you the steps through which you can pass all the Titanium detection of certificates.
<div><a href="http://skitch.com/yorzi/dutdc/preparation-iphone-provisioning-portal-apple-developer"><img src="http://img.skitch.com/20100825-b8ne3uxkfenjthcgnscecb89t.jpg" alt="Preparation - iPhone Provisioning Portal - Apple Developer" /></a><br /></div>
<br />
Then you will get the following files after your above configuration.
<div class="thumbnail"><a href="http://skitch.com/yorzi/dutrp/users-andy-desktop-apple-developer-app"><img src="http://img.skitch.com/20100825-ds2k13epf4b7grcmabr89yk11r.jpg" alt="/Users/andy/Desktop/apple_developer/app" /></a><br /></div>
<br />
After you import the above certificates to your keychain, you should see something similar in your Keychian.
<div class="thumbnail"><a href="http://skitch.com/yorzi/dutds/keychain-access"><img src="http://img.skitch.com/20100825-ra2mqhmcu94pk7kuxcpa7c6i2g.jpg" alt="Keychain Access" /></a><br /></div>
<br />
Finally, your Titanium will be the "ready status" for your debug and release on real device.
<div class="thumbnail"><a href="http://skitch.com/yorzi/dutfb/titanium-developer-1.2.1"><img src="http://img.skitch.com/20100825-m5b6ugwjywb66qggswbsumsmfk.jpg" alt="Titanium Developer (1.2.1)" /></a><br /></div>
<br />
The whole process might be painful unless you understand every concepts that Apple creates. I encounter problems when creating distribution provisioning profile. Only admin agent developer has permission to do so. Thus, you should ask admin agent for this provisioning profile, he can share this profile with a private key file, you import this key file to your Keychian, then you can distribute the app to whatever devices which is bundled into specific provisioning profile. 
