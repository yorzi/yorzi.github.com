--- 
layout: post
title: Rails Application Templates
comments: true
categories:
- rails
- Ruby On Rails
- templates
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
When talking about templates in Rails, usually people mean the templates which help to re-use views, but this templates is a <a href="http://github.com/rails/rails/commit/e8cc4b116c460c524961a07da92da3f323854c15">feature after Rails 2.3 for generating Rails application</a> easily, so give it a try if you haven't used it yet.

It's helpful for me to create Rails application according to similar skeleton, a sample below was written about one year ago, but recently I want to create a new application with the same environment/configuration.

<code lang="ruby">
#idapted_template.rb
generate :rspec

environment 'config.time_zone = "Beijing"'
environment 'config.i18n.default_locale = :zh'

name = ask("What's app's name?")
file 'config/site_config.yml', <<-CODE
app: #{name}
domain: mydomain
CODE

user = ask("What's db user name?")
pwd = ask("What's db user password?")
file 'config/database.yml', <<-CODE
development:
  adapter: mysql
  encoding: utf8
  database: #{name}_development
  user: #{user}
  password: #{pwd}
  pool: 5
  timeout: 5000

test:
  adapter: mysql
  encoding: utf8
  database: #{name}_test
  user: #{user}
  password: #{pwd}
  pool: 5
  timeout: 5000

production:
  adapter: mysql
  encoding: utf8
  database: #{name}_production
  user: #{user}
  password: #{pwd}
  pool: 5
  timeout: 5000
CODE

rake 'db:create:all'
rake 'db:sessions:create'
rake 'db:migrate'

gem 'idp_helpers'
gem 'idp_core'

run "rm public/index.html"

run "rm -rf tmp log"
run "svn import . http://mydomain.com/svn/projects/applications/#{name} -m 'add new app'"
run "rm -rf *"
run "svn checkout http://mydomain.com/svn/projects/applications/#{name} ."

file 'ignore_list', <<-CODE
log
tmp
nbproject
CODE
run "svn propset svn:ignore -F ignore_list ."
run "rm ignore_list"
run "svn commit -m 'set svn ignore'"
</code>

There are several useful commands which help you write powerful templates, you can learn more good examples <a href="http://m.onkey.org/2008/12/4/rails-templates">here</a>. or watch Ryan's Railscasts about <a href="http://railscasts.com/episodes/148-app-templates-in-rails-2-3">App Templates in Rails 2.3</a>.

Enjoy it.
