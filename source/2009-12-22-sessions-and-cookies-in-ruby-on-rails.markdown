--- 
layout: post
title: Sessions and Cookies in Ruby on Rails
comments: true
categories:
- cookie
- rails
- ror
- ruby
- Ruby On Rails
- session
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
<ol style="list-style-type: none; list-style-image: none; list-style-position: outside; margin-left: 0px;">
	<li>最近读了一篇文章，里面介绍了Session和Cookie在RoR开发中的使用方法，英文还不错的同学请<a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#scinrails" target="_blank">直接读这篇文章</a>。我仅仅在这篇Post里面做个整理，把那些有用的资料在此备份，免得下回又的麻烦Google。上面提到的文章很全面的介绍了很多细节，目录如下：
<ol style="list-style-type: none; list-style-position: outside; margin-left: 0px;">
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#sintro" target="_blank"><strong>Introduction</strong></a></li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#ssessions" target="_blank"><strong>Sessions</strong></a>
<ol style="margin-top: 0.4em; margin-right: 0.4em; margin-bottom: 1em; margin-left: 1.4em;">
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#sinrails" target="_blank">Session in rails</a></li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#sconfig" target="_blank">Configure your sessions</a></li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#sstorage" target="_blank">Storage options</a></li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#slimitations" target="_blank">Session storage limitations</a></li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#ssecurity" target="_blank">Session and Security</a></li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#showto" target="_blank">HowTo</a>
<ol style="margin: 0.4em;">
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#sexpire" target="_blank">Implement session expiration</a></li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#sstale" target="_blank">Delete stale sessions</a></li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#sactive" target="_blank">Find out active users</a></li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#ssessionid" target="_blank">Access session data using session_id</a></li>
</ol>
</li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#smisc" target="_blank">Miscellaneous</a></li>
</ol>
</li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#scookies" target="_blank"><strong>Cookies</strong></a>
<ol style="margin-top: 0.4em; margin-right: 0.4em; margin-bottom: 1em; margin-left: 1.4em;">
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#scinrails" target="_blank">Cookie on rails</a></li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#scvr" target="_blank">cookies vs. request.cookies</a></li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#scookiejar" target="_blank">CookieJar</a></li>
	<li><a style="color: #2244bb;" href="http://www.quarkruby.com/2007/10/21/sessions-and-cookies-in-ruby-on-rails#scmisc" target="_blank">Miscellaneous</a></li>
</ol>
</li>
</ol>
</li>
</ol>
