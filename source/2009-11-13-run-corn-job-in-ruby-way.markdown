--- 
layout: post
title: "Run cron job in Ruby way"
comments: true
categories:
- "定时任务"
- cron
- gem
- ruby
- Ruby On Rails
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
目前最常用的方法是利用Unix自身的<a href="http://en.wikipedia.org/wiki/Cron">cron</a>功能来实现定时任务，但是cron的语法比较麻烦(个人感觉)，今天为了执行一个定时任务发现了一个很好的RubyGem可以让你用Ruby的方式定义定时任务，这就是<a href="http://github.com/javan/whenever/tree/master">Whenever</a>。

Whenever可以让你写出类似下面的定时任务：
<pre name="code" class="ruby">
 set :cron_log, "/path/to/my/cron_log.log"

 every 2.hours do
   command "/usr/bin/some_great_command"
   runner "MyModel.some_method"
   rake "some:great:rake:task"
 end
</pre>
赶快去Github看看文档和代码吧<a href="http://github.com/javan/whenever">http://github.com/javan/whenever</a>
