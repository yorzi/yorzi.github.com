--- 
layout: post
title: create new user on CentOS
comments: true
categories:
- centos
- CentOS
- command
- Scripts
- useradd
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: ""
---
<strong>STUDY NOTES:</strong>

<strong>syntax:</strong>
useradd -s /bin/bash -d [folder_name]  -c “[name]” [userid]

<strong>sample:</strong>
useradd -s /bin/bash -d /home/andy -c "Andy Wang" andy

<strong>chagne password:</strong>
passwd andy
