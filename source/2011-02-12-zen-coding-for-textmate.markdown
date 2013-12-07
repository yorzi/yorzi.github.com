--- 
layout: post
title: Zen Coding for TextMate
comments: true
categories:
- bundle
- editor
- Environment
- Programing
- programming
- textmate
- zencoding
status: publish
type: post
published: true
meta: 
  aktt_notify_twitter: "no"
  _edit_last: "1"
  _wp_old_slug: ""
---
Bundles make <a href="http://macromates.com/">TextMate</a> as a super Editor, so if you love TextMate, you must love colorful bundles based on it.

I just find an interesting bundle to speed up your HTML/CSS coding, which is named as <a href="https://github.com/sergeche/zen-coding">Zen Coding</a>.

The core of this plugin is a powerful abbreviation engine which allows you to expand expressions—similar to CSS selectors—into HTML code. For example:
<code lang="html">
div#page>div.logo+ul#navigation>li*5>a
</code>
...can be expanded into:
<code lang="html">
<div id="page">
        <div class="logo"></div>
        <ul id="navigation">
                <li><a href=""></a></li>
                <li><a href=""></a></li>
                <li><a href=""></a></li>
                <li><a href=""></a></li>
                <li><a href=""></a></li>
        </ul>
</div>
</code>
The sytax is simple to understand, there is a sytax list <a href="http://code.google.com/p/zen-coding/wiki/ZenHTMLSelectorsEn">here</a>. You can also get more details about this bundle on <a href="http://code.google.com/p/zen-coding/">its official site.</a>

Enjoy it.
