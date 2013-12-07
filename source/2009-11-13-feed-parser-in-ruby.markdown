--- 
layout: post
title: Feed parser in Ruby
comments: true
categories:
- feedparser
- feedzirra
- gem
- Ruby
- ruby
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
<blockquote>There are a number of ways of parsing an RSS feed in Ruby, but one of the best is a gem called <a href="http://github.com/pauldix/feedzirra/tree/master">Feedzirra</a>. The main advantage of Feedzirra is its speed; it parses feeds very quickly, but it is also useful as it can parse many different types of feed.
</blockquote>

To install Feedzirra we first need to make sure that <code>http://gems.github.com</code> is in our list of gem sources. If not we’ll need to add it.
<pre>gem sources -a http://gems.github.com</pre>
Now we can install the gem:
<pre>sudo gem install pauldix-feedzirra</pre>
<strong><em>Notice:</em></strong> When I was installing the gem, there are several libs needed, including <em>libcurl4-gnutls-dev libcurl3-gnutls libxslt1-dev</em>, you may not meet this issue, it's not a big deal, just install what it rely on. Several dependencies will also be installed alongside the gem. Once everything’s installed we’ll need to add a reference to the gem in our application’s <em>/config/environment.rb</em> file.
<pre>config.gem "pauldix-feedzirra", :lib =&gt; "feedzirra", :source =&gt; "http://gems.github.com"</pre>
That’s it. We’re ready to start parsing RSS feeds in our application.

Getting start:
Assume that, you've got a model to store the feed content which is fetched by the parser, so the model should be like :
<pre name="code" class="ruby">
class FeedEntry < ActiveRecord::Base
  def self.update_from_feed(feed_url)
    feed = Feedzirra::Feed.fetch_and_parse(feed_url)
    add_entries(feed.entries)
  end

  private
  def self.add_entries(entries)
    entries.each do |entry|
      unless exists? :guid => entry.id
        create!(
          :name         => entry.title,
          :summary      => entry.summary,
          :url          => entry.url,
          :published_at => entry.published,
          :guid         => entry.id
        )
      end
    end
  end
end
</pre>
A more detailed manual is <a href="http://asciicasts.com/episodes/168-feed-parsing">here!</a>
