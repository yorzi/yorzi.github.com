--- 
layout: post
title: Performance Practice On Rails
comments: true
categories:
- cache
- fragment-cache
- memcached
- performance
- rails
- render-partial
- Ruby On Rails
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: cache-practice-on-rails
---
﻿﻿﻿﻿Last few days, I've been mainly struggling with performance issue which was sent to me on Monday. On Rails side, I didn't add enough necessary cache before I was told about the performance issue. Then I spent two days to improve it by adding cache every where I missed to do that before.

Some shares and confusions as below:

Shares:
1> A very useful educational website about scaling Rails where there are <a href="http://railslab.newrelic.com/2009/01/22/introduction">Scaling Rails Screencast Series</a> produced by Gregg Pollack and supported by New Relic.
2> Fragment cache.
      If you add many fragment cache in view, it's really a pain when you expire your cache, so I found there is a better way to expire your cache: if the cached block involves a model, for example, learner's sidebar involves "User" model's change, so I just name the cache with User model's "updated_at", so I don't need to expire this cache, it will be done automatically.
<code lang="ruby">
  <% cache("sidebar-profile-avatar-#{current_user.id}-#{current_user.updated_at.to_i}") do -%>
    <div class="sbb_title"><%= t :my_profile %></div>
    <div class="sbb_content">
      <table border="0" cellspacing="0" cellpadding="0" class="profile_table">
        <tr>
          <td width="100" rowspan="2" align="center" valign="top">
            <img src="<%= current_user.avatar_url || "/assets/images/portrait_demo.gif" %>" width="90" height="90" />
          </td>
          <td width="110" height="24"><%= display_learner([current_user], nil) %></td>
        </tr>
        <tr>
          <td valign="top"><strong><%= t :my_goal %></strong><%= display_oral_score(current_user.try(:study_info).try(:target_score)) %></td>
        </tr>
      </table>
    <% end -%>
</code>
3> Memcached. Cache whatever you want:
<code lang="ruby">
  def related_lessons
    cache_key = "related_lessons_for_item#{self.id}"
    return Rails.cache.read(cache_key) unless Rails.cache.read(cache_key).nil?
    if content_type == "Scenario"
      lessons = unit.extra_items.all(:conditions => {:content_id => content.extra_lessons.map(&:id)})
    elsif content_type == "ExtraLesson"
      lessons = [content.scenario.try(:item)]
    end
    Rails.cache.write(cache_key, lessons)
    return lessons
  end
</code>

Confusions:
1> It takes much time to render a partial view. that's pretty confusing to me. Some logs as below:
<code lang="ruby">
Cached fragment hit: views/sidebar-profile-roadmap-1268271150 (0.9ms)
Rendered shared/_sidebar_profile (109.8ms)
</code>
It seems like even the cached fragment is found, there still needs much time to render the partial..

2> From the log, I saw every request to "roadmap" index action will do the following stuff first, It's slow. But what that?
<code lang="ruby">
<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#<actionView::Base:0xb5a0e348>#
</code>

Any ideas on my confusions? All the involving clues are warmly welcomed.
