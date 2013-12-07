--- 
layout: post
title: Love named_scope
comments: true
categories:
- named_scope
- rails
- refactor
- Ruby On Rails
- snippet
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
Rails Best Practice Snippet: About named_scope.
Reference link to the PDF. <a rel="attachment wp-att-125" href="http://tech.wangyaodi.com/?attachment_id=125">Rails-best-practices.</a>

named_scope is a Rails 2.x feature which can simplify your rails code, move your finders into their own Model, and compact the code logically and gracefully. Below code refactoring is a named_scope sample to show the tricky.

<strong>BEFORE</strong>
<code lang="ruby">
class PostController < ApplicationController
  def search
    conditions = { :title => "%#{params[:title]}%" } if params[:title]
    conditions.merge!{ :content => "%#{params[:content]}%" } if params[:content]
    case params[:order]
      when "title" : order = "title desc"
      when "created_at" : order = "created_at"
    end
    if params[:is_published]
      conditions.merge!{ :is_published => true }
    end
    @posts = Post.find(:all, :conditions => conditions, :order => order,
                             :limit => params[:limit])
  end
end
</code>

<strong>AFTER</strong>
<code lang="ruby">
class Post < ActiveRecord::Base
  named_scope :matching, lambda { |column, value|
    return {} if value.blank?
    { :conditions => ["#{column} like ?", "%#{value}%"] }
  }
  named_scope :order, lambda { |order|
  { :order => case order
      when "title" : "title desc"
      when "created_at" : "created_at"
    end }
  }
end
</code>
<code lang="ruby">
class PostController < ApplicationController
  def search
    @posts = Post.matching(:title, params[:title])
                 .matching(:content, params[:content])
                 .order(params[:order])
  end
end
</code>

More references :
<a href="http://ryandaigle.com/articles/2008/3/24/what-s-new-in-edge-rails-has-finder-functionality">http://ryandaigle.com/articles/2008/3/24/what-s-new-in-edge-rails-has-finder-functionality</a>
<a href="http://railscasts.com/episodes/108-named-scope">http://railscasts.com/episodes/108-named-scope</a>
