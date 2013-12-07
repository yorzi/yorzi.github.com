--- 
layout: post
title: Formtastic for Rails
comments: true
categories:
- backup
- formtastic
- gems
- rails
- Ruby On Rails
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
<div>

I've been working on EQ portal during these days, I wanna share a useful gem which I used, it is called <a href="http://github.com/justinfrench/formtastic/tree/0.9.7">Formtastic</a>. it's a nice way to create form via formtastic, so the finial form is something like:
<code lang="ruby">
<% semantic_form_for @landing, :url=>admin_landings_path do |form| %>
  <p>
    <% form.inputs do %>
      <%= form.input :title, :label => 'Title' %>
      <%= form.input :url_slug, :label => 'Url slug' %>
      <%= form.input :meta, :label => 'Meta' %>
      <%= form.input :content, :label => 'Content' %>
    <% end %>
  </p>
  <p><%= form.buttons %></p>
<% end %>
</code>

Then it will generate HTML like this:
<code lang='ruby'>
<form action="/admin/landings" class="formtastic landing" id="new_landing" method="post"><div style="margin:0;padding:0;display:inline"><input name="authenticity_token" type="hidden" value="EC9WF1oK80Iq6X4NegSkBfVx5gLiYWvBEd7VeNKWHio=" /></div>
  <p>
    <fieldset class="inputs"><ol>
      <li class="string required" id="landing_title_input"><label for="landing_title">Title<abbr title="required">*</abbr></label><input id="landing_title" maxlength="255" name="landing[title]" size="30" type="text" /></li>
      <li class="string required" id="landing_url_slug_input"><label for="landing_url_slug">Url slug<abbr title="required">*</abbr></label><input id="landing_url_slug" maxlength="255" name="landing[url_slug]" size="30" type="text" /></li>
      <li class="text required" id="landing_meta_input"><label for="landing_meta">Meta<abbr title="required">*</abbr></label><textarea cols="40" id="landing_meta" name="landing[meta]" rows="20"></textarea></li>
      <li class="text required" id="landing_content_input"><label for="landing_content">Content<abbr title="required">*</abbr></label><textarea cols="40" id="landing_content" name="landing[content]" rows="20"></textarea></li>

    </ol></fieldset>
  </p>
  <p><fieldset class="buttons"><ol><li class="commit"><input class="create" id="landing_submit" name="commit" type="submit" value="Create Landing" /></li></ol></fieldset></p>
</form>
</code>
Also, it can be configured well in display style(not try yet), as well as working with this <a href="http://github.com/redinger/validation_reflection">validation plugin</a>

There is a more detailed Doc at: <a href="http://rdoc.info/rdoc/justinfrench/formtastic/blob/35eadf9a0f3e30101993419c3dd3327fb2fdd0b6/Formtastic/SemanticFormBuilder.html">http://rdoc.info/rdoc/justinfrench/formtastic/blob/35eadf9a0f3e30101993419c3dd3327fb2fdd0b6/Formtastic/SemanticFormBuilder.html</a>.  And samples at: <a href="http://asciicasts.com/episodes/184-formtastic-part-1">http://asciicasts.com/episodes/184-formtastic-part-1</a>

Enjoy it.</div>
