--- 
layout: post
title: perfect backup solution for developers
comments: true
categories:
- auto-backup
- backup
- db
- Gem/Plugin
- rails
- Ruby
- ruby
- S3
- Scripts
- whenever
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: ""
---
If you are system administrator, I know you are professional to write script doing flexible customized backup. But if you are like me as a Rails developer, and you just don't wanna spend too much time to struggle with tricky scripts for file or DB backup, you mush try my recommend backup solution on *nix system. Back to the topic : easy backup with "backup" and "whenever".

Yes, <a href="http://github.com/meskyanichi/backup">Backup</a> and <a href="http://github.com/javan/whenever">Whenever</a> is the best and easiest solution to manage your backup. They are all Ruby gems which are open sourced on github. Most of all, they are all working well both with Rails and with pure *nix environment. 

While using Backup, it's like a configuration file with easy rule, don't worry about the rule, I believe you will understand it in seconds. It also owns many common slots to different DB(or S3), you can also config your customized command and script inside its backup.rb file. Whenever is the Ruby way to manage your <a href="http://en.wikipedia.org/wiki/Cron">Cron</a> jobs, It's pretty cool.

Don't hesitate to try them out, you will find the inside beauty of backup. Enjoy! 
