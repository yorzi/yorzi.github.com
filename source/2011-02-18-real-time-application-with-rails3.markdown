--- 
layout: post
title: Real-Time Application with Rails3
comments: true
categories: 
- asynchronous
- chatting
- cramp
- eventmachine
- Gems/Plugin
- JavaScript
- juggernaut
- nodejs
- Programing
- Rails3
- real-time
- redis
- RTA
- RTC
- Ruby
- ruby
status: publish
type: post
published: true
meta: 
  aktt_notify_twitter: "no"
  _edit_last: "1"
  _wp_old_slug: ""
---
I researched a little bit these two days about Real-Time Application(RTA), I found many useful solution to build real-time application.

First, a RTA is an application program that functions within a time frame that the user senses as immediate or current. The latency must be less than a defined value, usually measured in seconds. The use of RTAs is called <a href="http://en.wikipedia.org/wiki/Real-time_computing">real-time computing</a> (RTC).

There are some example use cases of RTAs, including:
<pre>
   * Videoconference applications
   * VoIP (voice over Internet Protocol)
   * Online gaming
   * Community storage solutions
   * Chatting
   * IM (instant messaging)
</pre>
Mainly, I am interested in two solutions, which are <a href="https://github.com/lifo/cramp">Cramp</a> based RTA and a NR2J(<a href="http://nodejs.org/">Node.js</a>+<a href="https://github.com/antirez/redis">Redis</a>+<a href="https://github.com/maccman/juggernaut">Juggernaut</a>+Jquery) solution, both of these two solutions have existing samples, I suggest you should go through all of them to understand RTA well.

<strong>Cramp based RTA</strong>
Cramp is a ruby web framework with asynchronous feature, which is always running inside EventMachine reactor loop, there is a <a href="http://m.onkey.org/introducing-cramp">detailed introduction</a> for it. A sample code is <a href="https://github.com/akitaonrails/cramp_chat_demo">available here</a>.

<strong>NR2J solution</strong>
Introduction is <a href="http://www.golygon.com/2010/12/private-chat-room-in-ruby-on-rails-3-0/">here</a> and sample code is <a href="https://github.com/prabgupt/chatclient">here</a>. I tried Node.js before, it's getting popular recently, but I still don't be used to implementing server side code with JS. I love Ruby and Rails anyway.

<strong>Other RTA resources:</strong>
Real-Time/WebSocket/Rails3: <a href="http://laktek.com/tag/realie/">http://laktek.com/tag/realie/</a>
JSChat.org: <a href="http://jschat.org/">http://jschat.org/</a>


