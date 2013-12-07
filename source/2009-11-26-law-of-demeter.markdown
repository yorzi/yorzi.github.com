--- 
layout: post
title: Law of Demeter
comments: true
categories:
- delegate
- demeter
- model
- Programing
- rails
- refactor
- ruby
- Ruby On Rails
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
Rails Best Practice Snippet: Model refactor.
Reference link to the PDF.<a href='http://tech.wangyaodi.com/?attachment_id=125' rel='attachment wp-att-125'>Rails-best-practices.</a>

Before:
<code lang="ruby">
class Invoice < ActiveRecord::Base
  belongs_to :user
end
<%= @invoice.user.name %>
<%= @invoice.user.address %>
<%= @invoice.user.cellphone %>
</code>
After:
<code lang="rails">
class Invoice < ActiveRecord::Base
  belongs_to :user
  delegate :name, :address, :cellphone, :to => :user, :prefix => true
end
<%= @invoice.user_name %>
<%= @invoice.user_address %>
<%= @invoice.user_cellphone %>
</code>

See more details about <a href="http://api.rubyonrails.org/classes/Module.html#M000110">Delegate</a> in rails doc.
