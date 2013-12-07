--- 
layout: post
title: Rails3 App Gem Stack
comments: true
categories:
- Gem/Plugin
- gems
- plugin
- rails
- Rails3
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: ""
---
Rails3 RC1 was released yesterday, that's really awesome, I can't help experimenting a sample of Rails3 new features. I want to share my Gemfile to list all application gem stack, which may be useful for those who don't wanna create wheels themselves. Below is the list:
<code lang='ruby'>
# Bundle edge Rails instead:
gem 'rails', :git => 'git://github.com/rails/rails.git'

gem 'mysql'

# devise for auth
gem 'devise', '1.1.rc2'

# show_for is a helper for showing objects
gem 'show_for'

# pageinate
gem 'will_paginate', '3.0.pre'

# A set of responders modules to dry up your Rails 3 app
gem 'responders'

# Cron job in Rails
gem 'whenever', :git => 'git://github.com/javan/whenever.git'

# for creating navigations
gem 'simple-navigation', '2.6.0'

# for backup db to s3/remote server
gem 'backup', '2.3.2.pre3'

# Editor plugin
gem 'tiny_mce', '0.1.4'

# background job
gem "delayed_job","1.8.4"

# role based access control
gem "cancan"

# simple search on models
gem "searchlogic"

# full-text search solution
gem 'thinking-sphinx', '2.0.0.rc1', :require => 'thinking_sphinx'

# Use unicorn as the web server
gem 'unicorn'

# Deploy with Capistrano
gem 'capistrano'

# To use debugger
gem 'ruby-debug'

# Bundle the extra gems:
#gem 'bj'
gem 'nokogiri', '1.4.1'
# gem 'sqlite3-ruby', :require => 'sqlite3'
gem 'aws-s3', :require => 'aws/s3'

# Bundle gems for certain environments:
gem 'rspec', :group => :test
group :test do
  gem 'webrat'
end
</code>

If you wanna know whether a plugin/gem is available for Rails3, just check out this site: <a href="http://www.railsplugins.org/">http://www.railsplugins.org/</a> 
