--- 
layout: post
title: "Study Note : serialize object in ActiveRecord"
comments: true
categories: 
- activerecord
- Programing
- Ruby On Rails
- serialize
- study notes
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
<h2><span style="color: #444444; line-height: 24px; font-size: 16px;">Copied from <a href="http://api.rubyonrails.org/classes/ActiveRecord/Base.html#M001799" target="_blank">Ruby on Rails API doc</a>. Store here as a study notes for myself.

Active Record can <a href="Base.html#M001799">serialize</a> any object in text <a href="Base.html#M001809">columns</a> using YAML. To do so, you must specify this with a call to the class method <tt><a href="Base.html#M001799">serialize</a></tt>. This makes it possible to store arrays, hashes, and other non-mappable objects without doing any additional work. Example:</span></h2>
<pre>  class User &lt; ActiveRecord::Base
    serialize :preferences
  end

  user = User.create(:preferences =&gt; { "background" =&gt; "black", "display" =&gt; large })
  User.find(user.id).preferences # =&gt; { "background" =&gt; "black", "display" =&gt; large }</pre>
You can also specify a class option as the second parameter that‘ll raise an exception if a serialized object is retrieved as a descendant of a class not in the hierarchy. Example:
<pre>  class User &lt; ActiveRecord::Base
    serialize :preferences, Hash
  end

  user = User.create(:preferences =&gt; %w( one two three ))
  User.find(user.id).preferences    # raises SerializationTypeMismatch</pre>
