---
layout: post
title: "Install Jenkins and Set Up Jenkins CI for Rails Projects"
date: 2013-05-23 14:33
comments: true
categories: 
- Jenkins
- CI
- Rails
---

[Travis CI] is a great solution for OpenSource project, however, what if you want to setup an internal CI server for private projects? Believe or not, [Jenkins CI] is the choice. This post will guide you through the Jenkins installation and configuration on VPS (e.g. EC2 instance in this post) 

### OS Assumption 
Assume that you are running an EC2 instance with a Ubuntu system as below:

```
Ubuntu 12.04.2 LTS (GNU/Linux 3.2.0-40-virtual x86_64)
```

BTW, there is an Amazon [free tier] that is recommended if you don't have any VPS to use yet. 

### Install Rails Environment

As we mainly use this Jenkins CI server for Rails projects, so necessary Ruby/Rails libs and tools are needed as following:

#####- Install RVM and Ruby

We need to have git core and curl for [RVM] installation, so install them like this:

```
sudo apt-get install build-essential git-core
sudo apt-get install curl
```

And install [RVM] with ruby as user `jenkins`:

```
#remember to switch to user `jenkins` first
sudo su jenkins

curl -L https://get.rvm.io | bash -s stable --ruby
sudo apt-get install libmysqlclient-dev ruby-dev
```

#####- Install Possible Databases

######**MySQL**

```
sudo apt-get install mysql-client mysql-server libmysql-ruby libmysqlclient-dev
```

######Postgres
```
sudo aptitude install libpq-dev
sudo apt-get install postgresql
sudo apt-get install postgresql-client
```

If you had a problem with UTF-8 take a look at <http://wiki.gentoo.org/wiki/PostgreSQL>

###### MongoDB
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10
echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/10gen.list
sudo apt-get update
sudo apt-get install mongodb-10gen
```

### Install Jenkins

Installation:

```
wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo aptitude update
sudo aptitude install jenkins
```

Uninstall Jenkins is easy too, just:

```
sudo apt-get remove jenkins
```

There is also detailed [guide] for installing Jenkins on Ubuntu. FYI.


### Run Jenkins on Port 80

Default Jenkins runs on port 8080, you need to reverse proxy port 80 to port 8080 for Jenkins, it makes the CI server public to the world. To install nginx, open terminal and type in:

```
sudo apt-get install nginx
sudo /etc/init.d/nginx start
```

In order to Open up the config file in vim, and update it.

```
sudo vim /etc/nginx/nginx.conf
```

```
http {

        # ...Omitted Parts…

        include /etc/nginx/conf.d/*.conf;    # This line not modified.
        include /etc/nginx/sites-enabled/*;  # This line not modified.

        ##
        # Reverse proxy port 80 to port 8080 for Jenkins
        ##
        server {
                listen 80 default;
                server_name your.domain.com;
                location /{
                        proxy_pass http://127.0.0.1:8080;
                }
        }
} 
```

**Notice:** Jenkins shows build histories and other information, to keep the whole CI server private, you'd better use [this guide] to add basic auth for your Jenkins CI, it is strongly recommended.

### Install valuable plugins for Jenkins

Well, after above installations are done, you are able to visit your Jenkins CI server with your domain. Now it's time to install below plugins from `JenkinsPlugin > Manager` section:

- [Github Authentication plugin] is used for github OAuth. (This plugin has a bug that you can not logout some times.)
- [GitHub Plugin] integrates Jenkins with Github projects.
- [Jenkins Gravatar plugin] is used for showing Gravatar avatar images for Jenkins users.
- [RVM Plugin] runs your jobs in the RVM managed ruby+gemset of your choice.
- [Rake plugin] allows Jenkins to invoke Rake tasks as build steps.
- [All Changes Plugin] shows all changes which influenced the builds of a project.

For more plugins, you should check out the [Jenkins Plugins Document].


### References & Resources

<https://wiki.jenkins-ci.org/display/JENKINS/Configuring+a+Rails+build><br />
<http://aptobits.com/2012/09/setting-up-jenkins-ci-on-an-amazon-ec2-linux-instance/><br />
<http://watirmelon.com/2011/08/29/running-your-watir-webdriver-tests-in-the-cloud-for-free/><br />
<http://gistflow.com/posts/492-jenkins-ci-setup-for-rails-application-from-scratch><br />
<http://blogs.burnsidedigital.com/2013/01/setting-jenkins-ci-server-for-rails-project-on-a-vagrant-box/>

**NOTICE:** This is a blog I wrote for Intridea, I also post it here for my own reference. You are able to check out the [original post].

[Travis CI]: https://travis-ci.org/
[Jenkins CI]: http://jenkins-ci.org/
[RVM]: https://rvm.io/
[free tier]: http://aws.amazon.com/ec2/pricing/
[guide]: https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu
[this guide]: https://gist.github.com/yorzi/5590462
[Github Authentication plugin]: http://wiki.jenkins-ci.org/display/JENKINS/Github+OAuth+Plugin
[Jenkins Gravatar plugin]: http://wiki.jenkins-ci.org/display/JENKINS/Gravatar+Plugin]
[GitHub Plugin]: https://wiki.jenkins-ci.org/display/JENKINS/GitHub+Plugin
[RVM Plugin]: https://wiki.jenkins-ci.org/display/JENKINS/RVM+Plugin
[Rake plugin]: https://wiki.jenkins-ci.org/display/JENKINS/Rake+Plugin
[All Changes Plugin]: https://wiki.jenkins-ci.org/display/JENKINS/All+Changes+Plugin
[Jenkins Plugins Document]: https://wiki.jenkins-ci.org/display/JENKINS/Plugins
[original post]: http://www.intridea.com/blog/2013/5/21/howto-install-setup-jenkins-ci-for-rails-projects