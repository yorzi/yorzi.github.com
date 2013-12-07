--- 
layout: post
title: Install mysql on centOS5.5
comments: true
categories: 
- centos
- database
- installation
- mysql
- Mysql
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: ""
---
<strong>STUDY NOTES(<a href="http://library.linode.com/databases/mysql/centos-5" target="_blank">Linode VPS Doc Copy</a></strong><strong>):</strong>
<div id="installing-mysql">
<h2>Installing MySQL</h2>
Issue the following commands to update your system and install MySQL:
<pre>yum update
yum install mysql-server
/sbin/chkconfig --levels 235 mysqld on</pre>
The MySQL server package will be installed on your server, along with dependencies and client libraries. Start MySQL by running the following  command:
<pre>service mysqld start</pre>
</div>
<div id="configuring-mysql">
<h2>Configuring MySQL</h2>
After installing MySQL, it's recommended that you run <tt>mysql_secure_installation</tt>, a program that helps secure MySQL. While running <tt>mysql_secure_installation</tt>, you will be presented with the opportunity to change the MySQL root  password, remove anonymous user accounts, disable root logins outside of  localhost, and remove test databases. It is recommended that you answer yes to  these options. If you are prompted to reload the privilege tables, select yes. Run the following command to execute the program:
<pre>mysql_secure_installation</pre>
By default, MySQL makes some assumptions about your server  environment with respect to memory. To configure MySQL more conservatively, you'll need to edit some settings in the configuration file (<tt>/etc/my.cnf</tt>) as follows:
<pre>key_buffer = 16K
max_allowed_packet = 1M
thread_stack = 64K
table_cache = 4
sort_buffer = 64K
net_buffer_length = 2K</pre>
These settings are only suggested values for a low memory  environment; please feel free to tune them to appropriate values for your server. Consult the "More Information" section at the end of this tutorial for additional resources for this topic.

MySQL will bind to localhost (127.0.0.1) by default. Allowing unrestricted access to MySQL on a public IP not advised, but you may change the address it listens on by modifying the <tt>bind-address</tt> parameter. If you decide to bind MySQL to your public IP, you should implement firewall rules that only allow connections from specific IP addresses.

</div>
<div id="using-mysql">
<h2>Using MySQL</h2>
The standard tool for interacting with MySQL is the <tt>mysql</tt> client program. To get started, issue the following command at your prompt:
<pre>mysql -u root -p</pre>
You will be prompted to enter the root MySQL user's password. Enter the password you assigned when you installed MySQL, and you'll be presented with the MySQL monitor display:
<pre>Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 1
Server version: 5.0.45 Source distribution

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

mysql&gt;</pre>
Let's create a database and assign a user to it. Issue the following commands at the MySQL prompt:
<pre>CREATE DATABASE testdb;

CREATE USER 'testuser'@localhost IDENTIFIED BY 's8723hk2';

GRANT ALL PRIVILEGES ON testdb.* TO 'testuser'@localhost;

exit</pre>
Now let's log back into the MySQL client as <tt>testuser</tt> and create a sample table called "customers." Issue the following commands:
<pre>mysql -u testuser -p

USE testdb;

CREATE TABLE customers (customer_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, first_name TEXT, last_name TEXT);</pre>
This creates a table with a customer ID field of the type INT for integer (auto-incremented for new records, used as the primary key), as well as two fields for storing the customer's name. Of course, you'd probably want to store much more information than this on a customer, but it's a good example of a common case nonetheless.

</div>
<div id="resetting-the-mysql-root-password">
<h2>Resetting the MySQL  Root Password</h2>
If you've forgotten your root MySQL password, you may recover it by  issuing the following commands:
<pre>/etc/init.d/mysqld stop

mysqld_safe --skip-grant-tables &amp;

mysql -u root</pre>
The following part of the password reset will now be done within the  MySQL client program:
<pre>USE mysql;

UPDATE USER SET PASSWORD=PASSWORD("CHANGEME") WHERE USER='root';

FLUSH PRIVILEGES;

exit</pre>
Last, restart MySQL by issuing:
<pre>service mysqld restart</pre>
</div>
