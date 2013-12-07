--- 
layout: post
title: Overview of RenRen Connect Application
comments: true
categories:
- eq
- Renren
- ror
- SNS
- sns
- Web2.0
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
I’ve read <a href="http://wiki.dev.renren.com/wiki/%E9%A6%96%E9%A1%B5">RenRen development Doc</a> and tried some simple feature for a while, its platform is interesting and exciting, but much of its document is out of date(I guess it’s not been maintained for a time). so there are pains to test most of its APIs, here I will roughly introduce what we can do based on RenRen open platform.

First of all, RenRen platform supports <a href="http://wiki.dev.renren.com/wiki/%E5%90%8D%E8%AF%8D%E8%A7%A3%E9%87%8A">five types of APPLICATION</a>, which are:
– RenRen Canvas. It means application/content is embedded in RenRen’s web container via XNML/IFrame/OpenSocial-Gadget etc.
– Mobile Wap application.
– RenRen Connect. It means an external website is connected to RenRen, the two sites can share many different infos according to the channel/bridge API.
– Desktop Application.
– Mobile Client Application.

Obviously, RenRen Connect is what developer need upon first step. So the question is how does it work? Follow me, I will go through the imagined application to show what feature developer can build according to RenRen connect API, now go:

1. Tom is a RenRen user, he just find an “application” which tells him he can improve his oral English, that’s interesting, he clicks it in order to add the application to his list.

2. Then he find EQenglish.com, he uses his RenRen account to login EQenglish, He find he can order an speaking evaluation for free on the website, and what’s more, he even can push this message and/or the study status to his RenRen friends.

3. Tom goes through EQenglish website to check EQ learning methods, He can easily share the web page to his RenRen friends.

4. Andy is an EQenglish user, he bundles his EQ account and RenRen account on EQenglish website, so he can push his study status to his RenRen friends.

5. Andy finally buy a course, then all EQ learners who have RenRen accounts can receive an email/notification, in which it broadcasts “Andy buy a course ***” something like that.

6. Once Andy discussed an EQ lesson, his comments is synced to his RenRen status, all of his Friends there can see his status.

7. Tom finds Andy’s EQ profile via the discussion thread, the surprise is Andy’s is his School mate, they have the same IELTS exam time. They connect with each other on RenRen.

8. What’s more, Tom finds a section in EQ website, He can pick up all his Friends list, and suggest them to use EQ service. Also aside the lesson discussion thread, there is a live stream box connecting to RenRen page. so He can easily comment with friend..

Etc..

Above is a rough introduction of RenRen connect feature developer can build(it is based on RenRen connect’s API, not just my imagination).<a href="http://wiki.dev.renren.com/wiki/%E4%BA%A7%E5%93%81%E5%8A%9F%E8%83%BD%E8%AF%A6%E8%A7%A3">Click here to review RenRen Conncet Production Description.</a>
