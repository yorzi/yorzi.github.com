--- 
layout: post
title: "Study Notes: Passenger + Capistrano + Nginx + Rails 2.3.4 + Ubuntu 9.04 (10 steps)"
comments: true
categories:
- capistrano
- deploy
- Deployment
- nginx
- notes
- passenger
- rails
- Rails3
- Ruby On Rails
- Ubuntu
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
<strong><em>This post is just copied from </em></strong><a href="http://rustammamedov.wordpress.com/2009/12/27/capistrano-nginx-mongrel-deployment/"><strong><em>this page</em></strong></a><strong><em>. As a study notes, I re-share this manual here. Please check out original one if you wanna have a whole view of other involving topics. Thanks to the </em></strong><a href="http://rustammamedov.wordpress.com/"><strong><em>author</em></strong></a><strong><em> :)</em></strong>
<div>
<div>
<ol>
	<li>Install capistrano gem. if you use <a href="http://yehudakatz.com/2009/11/03/using-the-new-gem-bundler-today">bundler</a> you need to add just one line to Gemfile
<code>
gem "capistrano"
</code>
and then run
<code>gem bundle
</code></li>
	<li>after capistrano installed you need to make Capfile and default deploy.rb, run such from the root of your application
<code>capify .</code></li>
	<li>create user for deployments in remote machine (let’s say ‘deploy’ user)
<code>adduser deploy</code></li>
	<li>add sudo privileges to this user. add one line in your /etc/sudoers file
<code>deploy ALL=(ALL) NOPASSWD: ALL</code></li>
	<li>adjust deploy.rb for you. I used example from this <a href="http://jimneath.org/2008/05/10/using-capistrano-with-passenger-mod_rails/">link</a>
<code lang="ruby">
# Application
set :application, "test"
set :deploy_to, "/var/www/#{application}"
#	Settings
default_run_options[:pty] = true
set :use_sudo, true
#	Servers
set :user, "deploy"
set :domain, "rustam.example.com"
server domain, :app, :web
role :db, domain, :primary =&gt; true
#	Subversion
set :repository, "http://www.rustam.example.com"
set :svn_username, "rustam"
set :svn_password, "password"
set :checkout, "export"
#	Passenger
namespace :passenger do
desc "Restart Application"
task :restart do
run "touch #{current_path}/tmp/restart.txt"
end
end
after :deploy, "passenger:restart"
</code>
to understand how it works – read <a href="http://www.capify.org/index.php/Capistrano">this link</a></li>
	<li>if you don’t use bundler, skip it. Otherwise, it will be usefull to add such piece of code to your deploy.rb file (from <a href="http://gist.github.com/244420">Richie’s post</a>)
<code lang="ruby">
# bundler
namespace :bundler do
  task :install do
    run("gem install bundler --source=http://gemcutter.org")
  end
  
  task :symlink_vendor do
  shared_gems = File.join(shared_path, 'vendor/bundler_gems')
  release_gems = "#{release_path}/vendor/bundler_gems/"
    %w(cache gems specifications).each do |sub_dir|
      shared_sub_dir = File.join(shared_gems, sub_dir)
      run("mkdir -p #{shared_sub_dir} && mkdir -p #{release_gems} && ln -s #{shared_sub_dir} #{release_gems}/#{sub_dir}")
    end
  end

  task :bundle_new_release do
    bundler.symlink_vendor
    rails_env = variables[:rails_env] || 'production'
    run("cd #{release_path} && gem bundle --only #{rails_env}")
  end
end

after 'deploy:update_code', 'bundler:bundle_new_release'
</code>
it will bundle all production gems to your bundler_gems path</li>
	<li>ask Capistrano to create set of folders for deployments in the remote machine
<code>cap deploy:setup</code></li>
	<li>ask capistrano to check all remote folders:
<code>cap deploy:check</code>
it will return to you all problems that you have with both locale/remote machines – structure of folders/permissions etc. you can get something like this:
<code>
The following dependencies failed. Please check them and try again:
--&gt; You do not have permissions to write to `/var/www'. (rustam.example.com)
--&gt; You do not have permissions to write to `/var/www/releases'. (rustam.example.com)
</code>
When you’ll fix everything, you’ll get such:
<code>You appear to have all necessary dependencies installed</code>
it means that you’re finished with capistrano configs</li>
	<li>you need to install passenger and nginx module for passenger in your remote machine according to <a href="http://blog.phusion.nl/2009/04/16/phusions-one-year-anniversary-gift-phusion-passenger-220/">this</a>
<code>
sudo gem install passenger
sudo passenger-install-nginx-module</code>
the second command will tell you how to configure Nginx and to deploy rails application.
it will create Nginx configuration file for you:
<code>/opt/nginx/conf/nginx.conf)</code>
you need to change server block there
<code>
server {
listen 80;
server_name rustam.example.com;
root /var/www/current/public; # &lt;--- notice the 'public' part
passenger_enabled on; # &lt;--- don't forget this!li
}</code>
everything is finished for passenger and nginx!</li>
	<li>you can start deploy you app!
<code>cap deploy:update</code> – copies your project to remote machine and updates symlinks
<code>cap passenger-restart</code> – will start application</li>
FYI <code>sudo /opt/nginx/sbin/nginx</code> starts nginx in the remote machine
	<li><strong>Extra step</strong>: if you’re using bundler and used <a href="http://yehudakatz.com/2009/11/03/using-the-new-gem-bundler-today/">Yehuda’s link to run it</a>(like me <img src="http://s.wordpress.com/wp-includes/images/smilies/icon_smile.gif" alt=":)" /> ), you’ll have a problem with preinitializer. I used <a href="http://tomafro.net/2009/11/a-rails-template-for-gem-bundler">Tom Ward’s solution</a> to fix it
i.e. put only such line to preinitializer.rb
<code>require File.expand_path(File.join(File.dirname(__FILE__), "..", "gems", "environment"))</code>
and add such piece of code just after loading boot
<code>
# Hijack rails initializer to load the bundler gem
#environment before loading the rails environment.
Rails::Initializer.module_eval do
alias load_environment_without_bundler load_environment
def load_environment
Bundler.require_env configuration.environment
load_environment_without_bundler
end
end
</code></li>
</ol>
Links with detailed description:
<ul>
	<li><a title="http://wiki.zhekov.net/nginx" href="http://wiki.zhekov.net/nginx">nginx</a></li>
	<li><a title="http://gautamrege.wordpress.com/2009/11/10/capistrano-nginx-thin-deployment-on-linode" href="http://gautamrege.wordpress.com/2009/11/10/capistrano-nginx-thin-deployment-on-linode">capistrano-nginx-thin-deployment-on-linode</a></li>
	<li><a title="http://74.125.95.132/search?q=cache:NyrJDYo75rAJ:www.capify.org/index.php/From_The_Beginning+capistrano+from+the+beginning&amp;cd=2&amp;hl=en&amp;ct=clnk&amp;gl=us&amp;client=firefox-a" href="http://74.125.95.132/search?q=cache:NyrJDYo75rAJ:www.capify.org/index.php/From_The_Beginning+capistrano+from+the+beginning&amp;cd=2&amp;hl=en&amp;ct=clnk&amp;gl=us&amp;client=firefox-a">Capistrano from the beginning</a></li>
	<li><a title="http://www.viget.com/extend/building-an-environment-from-scratch-with-capistrano-2/" href="http://www.viget.com/extend/building-an-environment-from-scratch-with-capistrano-2/">capistrano + passenger</a></li>
	<li><a title="http://jimneath.org/2008/05/10/using-capistrano-with-passenger-mod_rails/" href="http://jimneath.org/2008/05/10/using-capistrano-with-passenger-mod_rails/">capistrano + passenger + mod_rails</a></li>
	<li><a title="http://www.rubyinside.com/28_mod_rails_and_passenger_resources-899.html" href="http://www.rubyinside.com/28_mod_rails_and_passenger_resources-899.html">28 links howto passenger + capistrano</a></li>
	<li><a title="http://blog.phusion.nl/2009/04/16/phusions-one-year-anniversary-gift-phusion-passenger-220/" href="http://blog.phusion.nl/2009/04/16/phusions-one-year-anniversary-gift-phusion-passenger-220/">passenger + nginx</a></li>
	<li><a title="http://www.modrails.com/documentation/Users%20guide%20Nginx.html" href="http://www.modrails.com/documentation/Users%20guide%20Nginx.html">nginx guide for passenger</a></li>
</ul>
</div>
</div>
