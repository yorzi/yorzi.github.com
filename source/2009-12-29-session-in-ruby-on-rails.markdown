--- 
layout: post
title: Session in Ruby on Rails
comments: true
categories:
- note
- ror
- Ruby On Rails
- session
- tech
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
<strong>session</strong>: a way to store information across pages.

<strong>set value as:</strong>
        session[:person] = ＠user

<strong>read values as:</strong>
        Hello #{session[:person]}

<strong>set as nil:</strong>
        session[:person] = nil

<strong>reset all sessions</strong>
        reset_session

There are many solutions to store session in ruby on rails, including
<strong>PStore</strong> [it's the default way in rails]
<strong>ActiveRecordStore</strong> [to use ActiveRecord, better to share information across apps in this way]
<strong>DRbStore</strong>
<strong>FileStore</strong>
<strong>MemoryStore</strong>


Much more compares on above solutions : check out <a href="http://scott.elitists.net/sessions.html">Ruby on Rails Session Container Performance</a> see the details.
