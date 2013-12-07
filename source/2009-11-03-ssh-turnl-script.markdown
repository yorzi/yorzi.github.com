--- 
layout: post
title: SSH tunnel script
comments: true
categories:
- dreamhost
- Scripts
- ssh
- tech
- tunnel
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
Why SSH tunneling?

Obviously, if you live in Chxna or some other place where you are restricted to access free network, and if you luckily own a ssh accessible account on a server that is hosted in a free country, congratulations, you can use ssh tunnel to fuck the wall.

Seriously, you just need to install ssh tool on your PC, (it will be much easier to setup a ssh tunnel if you are using a *nix OS), putty is a good choose if you are on Windows. I will show the script to explain what you should do on Ubuntu 9.04.
<pre name="code" class="ruby">
   ssh -qTfnN -D LocalPort remotehost(dreamhost)
</pre>
<code>
All the added options are for a ssh session that’s used for tunneling.
-q :- be very quite, we are acting only as a tunnel.
-T :- Do not allocate a pseudo tty, we are only acting a tunnel.
-f :- move the ssh process to background, as we don’t want to interact with this ssh session directly.
-N :- Do not execute remote command.
-n :- redirect standard input to /dev/null.
In addition on a slow line you can gain performance by enabling compression with the -C option.
</code>
 Enjoy it.
