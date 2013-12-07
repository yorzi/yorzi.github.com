--- 
layout: post
title: A note for building a simple Rails application
comments: true
categories:
- caches_page
- CMS
- EQV2
- feedzirra
- formtastic
- radiant
- ror
- routing
- Ruby On Rails
- Web2.0
- whenever
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: formtastic-routes-in-rails
---
最近花了一些时间改造公司的网站（<a href="http://www.eqenglish.com">EQV2</a>），这个网站是一个偏重内容和设计的信息类主站，并没有太多功能性的要求，所以在使用<a href="http://rubyonrails.org/">Ruby on Rails</a>开发这个网站的时候，尝试了一些之前涉及不多的技术。最初这个网站利用<a href="http://radiantcms.org/">Radiant</a>（RoR的开源CMS系统）搭建，考虑到没有专门的技术人员来管理和研究<a href="http://radiantcms.org/">Radiant</a>，而且和我们自己的系统平台的集成也会有些麻烦，最终决定放弃这把牛刀，仅仅做一个简单而且结构清晰的网站就OK。

我简单列一下这次改造过程中的一些比较典型的处理方法和技术：

* <a href="http://blog.wangyaodi.com/2009/12/22/formtastic-for-rails/">Formtastic</a> + nifty_scaffold
   用这两招可以方便的产生后台的CRUD管理部分，不知道为什么我第一反应没有使用<a href="http://activescaffold.com/">ActiveScaffold</a>，可能是从Rails2.3+以后Denny老说使用起来有问题有冲突，我就本能的绕开它了。
   参考： <a href="http://asciicasts.com/episodes/184-formtastic-part-1">http://asciicasts.com/episodes/184-formtastic-part-1</a>

* <a href="http://blog.wangyaodi.com/2009/11/13/feed-parser-in-ruby/">feedzirra</a> + <a href="http://blog.wangyaodi.com/2009/11/13/%E5%9C%A8ror%E4%B8%AD%E6%89%A7%E8%A1%8C%E5%AE%9A%E6%97%B6%E4%BB%BB%E5%8A%A1/">whenever</a>
  feedzirra是一个方便易用的RSS分析器，很不错，结合whenever就可以自动更新源RSS，在我们的系统中我用它们更新Blog中的内容到网站上面来。
   参考： <a href="http://github.com/pauldix/feedzirra">http://github.com/pauldix/feedzirra</a>
              <a href="http://github.com/javan/whenever/">http://github.com/javan/whenever/</a>

* <a href="http://code.google.com/p/rubycas-server/">cas</a>
   <a href="http://www.dujinfang.com">7哥</a>搭建了一个idp_cas的server，我就结合这个做了一个单点登录的控制，用来对后台内容管理做权限控制。这个方案很轻量级，避免了直接集成复杂的idp用户验证系统。

* Routing
   此次最想突出介绍的是ROR的<a href="http://api.rubyonrails.org/classes/ActionController/Routing.html">Routing</a>机制，强大的Routing可以将URL改写成任何形式，以适应SEO的需要，同时也可以做坏链的容错处理。很好很强大，就是不知道效率如何，这个有待进一步熟悉。

* caches_page
   由于本次改造过程中主要涉及内容性质的View，所以我只进行了Page Cache，Rails的Cache方法也很简单易用，我稍后会做一个较为详细的总结，讨论一下各种Cache的问题。

此次改造的重点是网站结构和UI/UE的设计，Noah和Buzz主要负责这方面的工作，正因为他们出色的工作成果才使得EQV2顺利按期交付。
