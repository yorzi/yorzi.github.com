--- 
layout: post
title: mysql dump
comments: true
categories: 
- bz2
- dump
- mysql
- Mysql
- script
- tech
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
I'm a little shamed that I ask Sonic for a mysql dump command several times, I rarely dump db myself, that's why I forget the way dealing with it.. Ok, the commands are:
<pre name="code" class="mysql">
mysqldump -u root user_production > user_production.sql
bzip2 user_production.sql

scp from server to local.

bunzip2 user_production.sql.bz2
bzcat user_production.sql.bz2 | mysql -u root user_production
or extracts the backup files, to create db directly.
</pre>

Thanks Sonic.
