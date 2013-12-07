--- 
layout: post
title: Ajax Support in Rails
comments: true
categories:
- ajax
- JavaScript
- javascript
- prototype
- rails
- RJS
- Ruby On Rails
- scriptaculous
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
<strong>Topics</strong>
  Ajax/JavaScript libraries in Rails
  PrototypeHelper
  ScriptaculousHelper
  JavaScriptMacrosHelper
  JavaScript related utility methods
  Ruby JavaScript template

<strong>Ajax/JavaScript Libraries in Rails</strong>
• Prototype - used mainly for Ajax
  > ActionView::Helpers::PrototypeHelper
• Scriptaculous - used mainly for visual effects, drag and drop, auto-completion
  > ActionView::Helpers::ScriptaculousHelper
• JavaScript related utility methods
  > ActionView::Helpers::JavaScriptHelper
• Others can be easily added

<strong>How to Include Ajax?JavaScript Libraries</strong>
• Option 1: Use <%= javascript_include_tag :defaults %> in the HEAD section of your page (recommended):
   > Return references to the JavaScript files in your public/javascripts directory.
   > Recommended as the browser can then cache the libraries instead of fetching all the functions anew on every request.
• Option 2: Use <%= javascript_include_tag ‘prototype’ %>
   > Will only include the Prototype core library
• Option 3: Use <%= define_javascript_functions %>
   > Will copy all the JavaScript support functions within a single script block. Not recommended.

SEE MORE DETAILS VIA <a href='http://tech.wangyaodi.com/?attachment_id=136' rel='attachment wp-att-136'>Download the PDF</a> stuff.
