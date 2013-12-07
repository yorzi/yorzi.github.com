--- 
layout: post
title: "Script: Fetch parameter value from url"
comments: true
categories: 
- JavaScript
- js
- query string
- snippet
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: ""
---
I wanna get the query string value, and set it to specific element, how to do that by javascript?
Say, http://sample.com?author=andy, how to get author value which can be lately used. see the script below:
<pre><code land='javascript'>
        function fetch_value(name)
        {
          name = name.replace(/[\[]/,'\\\[').replace(/[\]]/,'\\\]');
          var regexS = '[\\?&]' + name+'=([^&#]*)';
          var regex = new RegExp( regexS );
          var results = regex.exec( window.location.href );
          if( results == null )
            return '';
          else
            return results[1];
        }
</code></pre>
Then you should use this function as fetch_value("author"), it will return the "andy".
