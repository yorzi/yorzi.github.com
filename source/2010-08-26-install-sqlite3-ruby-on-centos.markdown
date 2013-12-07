--- 
layout: post
title: install sqlite3-ruby on CentOS
comments: true
categories:
- centos
- CentOS
- gem
- Ruby
- ruby-gem
- sqlite3
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
Normally you would get an error if you try to install or to update your sqlite3-ruby gems. But you need this gem when there is other dependence. Here’s the solution to get it running:

Go to sqlite.org and get the amalgamation package or wget directly (below is my way):
<pre>
# cd into my source tarball folder
cd /usr/src
# get the amalgation package
wget http://sqlite.org/sqlite-amalgamation-3.6.23.1.tar.gz
# unpack it
tar xvzf sqlite-amalgamation-3.6.23.1.tar.gz
# cd into the created folder
cd sqlite-amalgamation-3.6.23.1
# run configuration
./configure
# make and intall the package
make && sudo make install
</pre>
After successfully install the installer will tell where the library files have been stored in. In my case this was “/usr/local/lib”.

So I can install the gem now with:
<pre>
gem install sqlite3-ruby — –with-sqlite3-include=/usr/local/include \
–with-sqlite3-lib=/usr/local/lib
</pre>
# getting this as a result
Building native extensions. This could take a while…
Successfully installed sqlite3-ruby-1.3.1
1 gem installed

Ok, done.
