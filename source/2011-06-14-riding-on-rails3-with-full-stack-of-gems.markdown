--- 
layout: post
title: Riding on Rails3 with full stack of Gems
comments: true
categories: 
- gems
- Gems/Plugin
- Rails3
status: publish
type: post
published: true
meta: 
  _cws_is_markdown: "1"
  _edit_last: "1"
  aktt_notify_twitter: "no"
---
<strong>NOTICE:</strong> Below post was released a month ago on <a href="http://intridea.com/2011/5/13/rails3-gems">Intridea Company Blog</a>, also post here as a backup.

It's been close to a year since Rails3 came out. Luckily, I've worked on several Rails3 projects after it's released, so I'd like to share a stack of gems that I used in my previous projects. I guess they will give people a bit help while developing a new Rails3 app.

I don't want to explain too much on these gems separately, well, most of the gems have good documents on their project wiki(every great gem should be well documented, right?). Instead, I just add regarding links to their repos so that you'd better take a further look while you really use it. In order to introduce the lists of gems clearly, I simply categorized them based on a rough structure.

Ok, here we start:

<h4><strong>&raquo; Authentication</strong></h4>

<blockquote>
  <ul>
  <li>OmniAuth (<a href="https://github.com/intridea/omniauth">https://github.com/intridea/omniauth</a>)</li>
  <li>Devise (<a href="https://github.com/plataformatec/devise">https://github.com/plataformatec/devise</a>)</li>
  </ul>
</blockquote>

The above two are really amazing gems to speed up your authentication. Yes, I love both of them in different cases: ideally OmniAuth is better for applications which want to support multi-provider external authentication, so I've just added OmniAuth into RefactorMyCode Rails3 branch to take its auth benefits; Devise is totally powerful enough for classic authentication case. However, if you have too much your own business logic inside your login/registration/auth flow, you definitely need to make your own authentication.

<h4><strong>&raquo; Access Control</strong></h4>

<blockquote>
  <ul>
  <li>CanCan (<a href="https://github.com/ryanb/cancan">https://github.com/ryanb/cancan</a>)</li>
  <li>declarative_authorization (<a href="https://github.com/stffn/declarative_authorization">https://github.com/stffn/declarative_authorization</a>)</li>
  </ul>
</blockquote>

<a href="https://github.com/ryanb">Ryan</a> is a star in Rails world, so his CanCan is really popular, which aims to do neat but powerful authorization. However, the declarative_autharization is also an option, actually, Ryan mentioned CanCan was inspired by declarative_autharization.

<h4><strong>&raquo; Views/Page and Admin Scaffold</strong></h4>

<blockquote>
  <ul>
  <li>compass (<a href="https://github.com/chriseppstein/compass">https://github.com/chriseppstein/compass</a>)</li>
  <li>haml (<a href="https://github.com/nex3/haml">https://github.com/nex3/haml</a>)</li>
  <li>sanitize (<a href="https://github.com/rgrove/sanitize">https://github.com/rgrove/sanitize</a>)</li>
  <li>rails_admin (<a href="https://github.com/sferik/rails_admin">https://github.com/sferik/rails_admin</a>)</li>
  <li>web-app-theme (<a href="https://github.com/andreferraro/web-app-theme">https://github.com/andreferraro/web-app-theme</a>)</li>
  </ul>
</blockquote>

From a front-end perspective, I suggest you might need to try above gems to speed up and simplify your UI designing. For example on the admin section, it'd be great if you can apply your CRUD quickly to pages, that's what rails_admin does. Surely, these gems won't end all your UI problems, but it really helps when you doing prototype or being lack of some real designers.

<h4><strong>&raquo; Quick SNS</strong></h4>

<blockquote>
  <ul>
  <li>acts-as-taggable-on (<a href="https://github.com/mbleigh/acts-as-taggable-on">https://github.com/mbleigh/acts-as-taggable-on</a>)</li>
  <li>has_friends-rails3 (<a href="https://github.com/rrouse/has_friends">https://github.com/rrouse/has_friends</a>)</li>
  <li>acts_as_favable (<a href="https://github.com/yorzi/acts_as_favable">https://github.com/yorzi/acts_as_favable</a>)</li>
  <li>thumbs_up (<a href="https://github.com/brady8/thumbs_up">https://github.com/brady8/thumbs_up</a>)</li>
  <li>acts_as_commentable (<a href="https://github.com/jackdempsey/acts_as_commentable">https://github.com/jackdempsey/acts_as_commentable</a>)</li>
  <li>profanity_filter (<a href="https://github.com/intridea/profanity_filter">https://github.com/intridea/profanity_filter</a>)</li>
  </ul>
</blockquote>

Well, I don't mean a whole solution of SNS or regarding feature, here theses gems can help you add the basic cross-object function rapidly, it increases your confidence to focus on designing over programming at the very beginning. Here I want to give a simple introduction to <strong>acts_as_favable</strong>, it allows for favorites refer to be added to multiple and different models.

<h4><strong>&raquo; Form and Related Tools</strong></h4>

<blockquote>
  <ul>
  <li>simple_form (<a href="https://github.com/plataformatec/simple_form">https://github.com/plataformatec/simple_form</a>)</li>
  <li>formtastic (<a href="https://github.com/justinfrench/formtastic">https://github.com/justinfrench/formtastic</a>)</li>
  <li>formtastic_datepicker_inputs (<a href="https://github.com/demersus/formtastic_datepicker_inputs">https://github.com/demersus/formtastic_datepicker_inputs</a>)</li>
  <li>tiny_mce (<a href="https://github.com/kete/tiny_mce">https://github.com/kete/tiny_mce</a>)</li>
  <li>paperclip (<a href="https://github.com/thoughtbot/paperclip">https://github.com/thoughtbot/paperclip</a>)</li>
  <li>carrierwave (<a href="https://github.com/jnicklas/carrierwave">https://github.com/jnicklas/carrierwave</a>)</li>
  </ul>
</blockquote>

Most of above gems are famous through &lt;railscasts.com> created by Ryan. There are two pairs of options here: <strong>simple_form</strong> and <strong>formtastic</strong> / <strong>paperclip</strong> and <strong>carrierwave</strong>. I like all these solutions, you should pick up one to fit your project, if you want to know differences between each pair, get more details on their wiki :) Tiny is an HUGE gem for rich editing, I list it here to remind its exist, but I recommend you  get the WYSWYG via some JS lib like <a href="http://premiumsoftware.net/cleditor">CLEditor</a>, it works gracefully.

<h4><strong>&raquo; Searching Solutions</strong></h4>

<blockquote>
  <ul>
  <li>meta_seach (<a href="https://github.com/ernie/meta_search">https://github.com/ernie/meta_search</a>)</li>
  <li>meta_where (<a href="https://github.com/ernie/meta_where">https://github.com/ernie/meta_where</a>)</li>
  <li>thinking-sphinx (<a href="https://github.com/freelancing-god/thinking-sphinx">https://github.com/freelancing-god/thinking-sphinx</a>)</li>
  <li>acts_at_indexed (<a href="https://github.com/dougal/acts_as_indexed">https://github.com/dougal/acts_as_indexed</a>)</li>
  <li>sunspot (<a href="https://github.com/outoftime/sunspot">https://github.com/outoftime/sunspot</a>)</li>
  </ul>
</blockquote>

Talking about searching in rails, I think you have many words to say. Here I wanna roughly split these gems into two types: Object-based searching and Full-Text searching. I heavily recommend you use meta_search and/or meta_where as your model based searching, it can convert your form params directly to a search solution, that's convenient. Full-Test searching depends on your case, but all these three gems(thinking-sphinx, acts_as_indexed, sunspot) are great.

<h4><strong>&raquo; Pagination</strong></h4>

<blockquote>
  <ul>
  <li>kaminari (<a href="https://github.com/amatsuda/kaminari">https://github.com/amatsuda/kaminari</a>)</li>
  <li>kaminari_themes (<a href="https://github.com/amatsuda/kaminari_themes">https://github.com/amatsuda/kaminari_themes</a>)</li>
  </ul>
</blockquote>

No more will_paginate in Rails3, absolutely, the only option is kaminari.

<h4><strong>&raquo; Background Work</strong></h4>

<blockquote>
  <ul>
  <li>delayed_job (<a href="https://github.com/collectiveidea/delayed_job">https://github.com/collectiveidea/delayed_job</a>)</li>
  <li>resque (<a href="https://github.com/defunkt/resque">https://github.com/defunkt/resque</a>)</li>
  </ul>
</blockquote>

There is one post to introduce resque clearly <a href="https://github.com/blog/542-introducing-resque">here</a>, in that post, github staff mentioned their brief history of doing background jobs, so I think you can understand well the differences between delayed_job and resque solution.

<h4><strong>&raquo; Status Machine</strong></h4>

<blockquote>
  <ul>
  <li>workflow (<a href="https://github.com/ryan-allen/workflow">https://github.com/ryan-allen/workflow</a>)</li>
  <li>state_machine (<a href="https://github.com/pluginaweek/state_machine">https://github.com/pluginaweek/state_machine</a>)</li>
  </ul>
</blockquote>

I like to use workflow a bit more, since it's much natural to me, you definitely need one status machine to control your stable flow stuff, such as a registration flow status or a wizard-like features.

<h4><strong>&raquo; Rack API framework</strong></h4>

<blockquote>
  <ul>
  <li>grape (<a href="https://github.com/intridea/grape">https://github.com/intridea/grape</a>)</li>
  </ul>
</blockquote>

This gem is for adding API to Rails/Sinatra application. <a href="http://intridea.com/about/people/mbleigh">Michael</a> gave people an awesome <a href="http://confreaks.net/videos/475-rubyconf2010-the-grapes-of-rapid">speech in RubyConf2010</a> on his Grape, here I suggest you should watch it to know more details about GRAPE. I believe you will fall in love with it.

<h4><strong>&raquo; Memcached Client</strong></h4>

<blockquote>
  <ul>
  <li>memcache-client (<a href="https://github.com/mperham/memcache-client">https://github.com/mperham/memcache-client</a>)</li>
  <li>dalli (<a href="https://github.com/mperham/dalli">https://github.com/mperham/dalli</a>)</li>
  </ul>
</blockquote>

These two gems are actually mainly written by one same author <em><a href="https://github.com/mperham">Mike Perham</a></em>, he mentioned that <em>Dalli is a high performance pure Ruby client for accessing memcached servers. It works with memcached 1.4+ only as it uses the newer binary protocol. It should be considered a replacement for the memcache-client gem. The API tries to be mostly compatible with memcache-client with the goal being to make it a drop-in replacement for Rails.</em>

<h4><strong>&raquo; Deployment and Monitor</strong></h4>

<blockquote>
  <ul>
  <li>capistrano (<a href="https://github.com/capistrano/capistrano">https://github.com/capistrano/capistrano</a>)</li>
  <li>cap-recipes (<a href="https://github.com/nesquena/cap-recipes">https://github.com/nesquena/cap-recipes</a>)</li>
  <li>god (<a href="https://github.com/mojombo/god">https://github.com/mojombo/god</a>)</li>
  </ul>
</blockquote>

I am not a system administrator, so every time talking about the regarding aspects will make me feel silly, I just try to describe tools which can help me out on unfamiliar area, that's not bad, at least people like me, will do deployment and monitor quickly based on these gems, they do help.

<h4><strong>&raquo; Cron job and Backup as a Pro</strong></h4>

<blockquote>
  <ul>
  <li>whenever (<a href="https://github.com/javan/whenever">https://github.com/javan/whenever</a>)</li>
  <li>backup (<a href="https://github.com/meskyanichi/backup">https://github.com/meskyanichi/backup</a>)</li>
  </ul>
</blockquote>

Above two gems are my favorites, before knowing these two gems, I have to write complex and stupid scripts to do backups that I am not familiar with. Cron job is also a pain in ass if you are not a system administrator. Now time changes, you, as a ruby programmer, can do the corn job and backup in ruby way, surely as a PRO. :)

<h4><strong>&raquo; Testing Gracefully</strong></h4>

<blockquote>
  <ul>
  <li>rspec-rails (<a href="https://github.com/dchelimsky/rspec-rails">https://github.com/dchelimsky/rspec-rails</a>)</li>
  <li>factory_girl_rails (<a href="https://github.com/thoughtbot/factory_girl_rails">https://github.com/thoughtbot/factory_girl_rails</a>)</li>
  <li>faker (<a href="https://github.com/yyyc514/faker">https://github.com/yyyc514/faker</a>)</li>
  <li>watchr (<a href="https://github.com/mynyml/watchr">https://github.com/mynyml/watchr</a>)</li>
  <li>autowatchr (<a href="https://github.com/viking/autowatchr">https://github.com/viking/autowatchr</a>)</li>
  <li>database_cleaner (<a href="https://github.com/bmabey/database_cleaner">https://github.com/bmabey/database_cleaner</a>)</li>
  <li>mail_safe (<a href="https://github.com/myronmarston/mail_safe">https://github.com/myronmarston/mail_safe</a>)</li>
  </ul>
</blockquote>

Testing is always important, I know TDD and BDD are getting more and more popular, that means you have to own your super gun to make it happen. Right, here is a list of gems which can help you out, I didn't cover all different levels of testing with these gems. Point is, rspec is my favorite framework for testing, <strong>factory_girl</strong> and <strong>faker</strong> are good supports. Anyway, test by your way.

<h4><strong>&raquo; Toolkit</strong></h4>

<blockquote>
  <ul>
  <li>ruby-debug (<a href="https://github.com/mark-moseley/ruby-debug">https://github.com/mark-moseley/ruby-debug</a>)</li>
  <li>hirb (<a href="https://github.com/cldwalker/hirb">https://github.com/cldwalker/hirb</a>)</li>
  <li>cheat (<a href="https://github.com/defunkt/cheat">https://github.com/defunkt/cheat</a>)</li>
  <li>rails-settings-cached (https://github.com/huacnlee/rails-settings-cached)</li>
  </ul>
</blockquote>

There are many handy gems which will give you convenience and power. Take above four as examples, ruby-debuy gives you a chance to check your running applications' context at specific program point; hirb display your AR items in table view in console; cheat makes your terminal working as a pool of other gems' manual; rails-settings-cached is for global configurations in Rails3 application. Yeah, throwing the brick out is to meet your GEMS.

<h3><strong>How to find great gems?</strong></h3>

First, you need to follow up Ryan's <a href="railscasts.com">railscasts</a>, he is good at introducing new stuff in video. Second, you can go through great open source project's <strong>Gemfile</strong>, yeah, it's definitely the best way to come across valuable gems. Third, just subscribe <a href="https://github.com/languages/Ruby">github ruby trends</a> to know what's going on in Ruby/Rails community. There are also some other involving sites, like <a href="rubygems.org">rubygems</a> and <a href="railsplugins.org">railsplugins</a>, you should take a glance when you free, I bet you will find useful gems.

It's nearly the end of this post, this topic was originally shared with all Intridea China Team members during last Friday Teahour. You can find the PPT <a href="http://www.slideshare.net/yorzi/riding-on-rails3-with-full-stack-of-gems">here</a>. To share with more people, I turn it into this blog, I must miss many valuable gems in this list, so please comment your thoughts.
