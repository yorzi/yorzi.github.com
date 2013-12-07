--- 
layout: post
title: Dalli on Rails3
comments: true
categories:
- cache
- dalli
- Gem/Plugin
- memcached
- memcached client
- Performance
- rails
- Rails3
status: publish
type: post
published: true
meta: 
  aktt_notify_twitter: "no"
  _edit_last: "1"
  _wp_old_slug: ""
---
Today I tried a new pure Ruby <a href="http://memcached.org/" target="_blank">memcahed</a> client in one of my Rails3 projects, it's named as "<a href="https://github.com/mperham/dalli" target="_blank">Dalli</a>". It's an excellent memcached client as <a href="http://www.mikeperham.com/">Mike Perham</a> announced in August last year. You can detect more details about it on its code. Dalli is just faster performance than memcache-client and easy to use in Rails3 or on <a href="http://heroku.com" target="_blank">Heroku</a>.

Make sure you've installed 1.4+ memcached on your machine, then you can configure Dalli as what you did with memcache-client before:
1. add gem in Gemfile
<code lang="ruby">
gem 'dalli'
</code>
2. Config the underlying cache store as dalli_store in production.rb
<code lang="ruby">
#Memcached is delaulted on port 11211.
config.cache_store = :dalli_store, 'localhost:11211'
</code>
3. Now you will find the Rails.cache class is changed to Rails.cache.class:
<code lang="ruby">
>> Rails.cache.class
== ActiveSupport::Cache::DalliStore
</code>
4. You can use it easily in you Rails3 application
<code lang="ruby">
class Food < ActiveRecord::Base
   after_save :expire_food_caches

   def self.all_view_types
      Rails.cache.fetch("food_types") do
          Food.all.map{|s| s.view_type}.uniq
      end
   end

   protected
   def expire_food_caches
       unless Food.all_view_types.include?(self.view_type)
           Rails.cache.delete("food_types")
       end
   end
end
</code>
<em><strong>Note</strong>: Rails.cache.fetch() with a block will return the cached value if it exists, otherwise it will return the value and write cache with the value at the same time.</em>

Resource about Cache:
Scaling Rails : <br /><a href="http://railslab.newrelic.com/scaling-rails">http://railslab.newrelic.com/scaling-rails</a>
Caching with Rails : <br /><a href="http://guides.rubyonrails.org/caching_with_rails.html">http://guides.rubyonrails.org/caching_with_rails.html</a>
ActiveSupport::Cache::Store : <br /><a href="http://api.rubyonrails.org/classes/ActiveSupport/Cache/Store.html#method-i-clear">http://api.rubyonrails.org/classes/ActiveSupport/Cache/Store.html#method-i-clear</a>
ActiveSupport::Memoizable : <br /><a href="http://ilstar.blogbus.com/logs/84754288.html#cmt">http://ilstar.blogbus.com/logs/84754288.html#cmt</a>
