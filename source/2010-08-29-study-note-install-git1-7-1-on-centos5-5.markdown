--- 
layout: post
title: "Study Note: Install Git1.7.1 on CentOS5.5"
comments: true
categories:
- CentOS
- Environment
- git
- libiconv
- study notes
- tips
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: ""
---
Step 1. Install the dependencies
<pre>
$ sudo yum -y install curl-devel expat-devel \
gettext-devel openssl-devel zlib-devel  
$ wget http://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.13.1.tar.gz  
$ tar zxf libiconv-1.13.1.tar.gz  
$ cd libiconv-1.13.1  
$ ./configure prefix=/usr/local  
$ make  
$ sudo make install
</pre>
Step 2. Install Git1.7.1
<pre>
$ wget http://kernel.org/pub/software/scm/git/git-1.7.1.tar.gz  
$ tar zxf git-1.7.1.tar.gz  
$ cd  git-1.7.1  
$ ./configure prefix=/usr/local
$ make
$ sudo make install 
</pre>
Step 3. You might get errors as:
<pre>error while loading shared libraries: libiconv.so.2:\
cannot open shared object file: No such file or directory</pre>
Then, you should do the following:
<pre>
$ sudo vim /etc/ld.so.conf
# you should add online as "/usr/local/lib"
$ sudo /sbin/ldconfig
</pre>
Done, try git --version, it's successfully installed.
