--- 
layout: post
title: Set static IP on Ubuntu
comments: true
categories: 
- ip
- network
- tech
- ubuntu
- Ubuntu
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
Edit:
<code>sudo vim /etc/network/interfaces</code>

Then change the content, assuming you want to set your IP as "192.168.1.66"
<code># The primary network interface
auto eth0
iface eth0 inet static
        address 192.168.1.66
        netmask 255.255.255.0
        network 192.168.1.0
        broadcast 192.168.1.255
        gateway 192.168.1.1
</code>

Then to restart your network.
<code>sudo /etc/init.d/networking restart</code>
