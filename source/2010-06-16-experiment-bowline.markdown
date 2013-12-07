--- 
layout: post
title: Experiment Bowline
comments: true
categories:
- bowline
- css3
- desktop
- Html5
- JavaScript
- mvc
- Rails3
- Ruby
- ruby
- rvm
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: ""
---
<blockquote>Bowline is a framework for making cross platform desktop applications in Ruby, HTML and JavaScript.

If you've ever wished creating a desktop application was as simple as creating a Rails website, Bowline's for you.

Bowline respects MVC, you can design your views in HTML5/CSS3 - then bind them to your Ruby models. There's no request/response cycle - any changes in models automatically get reflected in the view.</blockquote>
<p style="text-align: right;"><strong>See : <a href="http://bowlineapp.com/">http://bowlineapp.com/</a></strong></p>
Experiment on this framework:

<strong>Requirements:</strong>

* Mac OSX &gt;=10.5 or Ubuntu -----&gt; [I am on Ubuntu 9.04]
* Ruby 1.9 -----------------------------&gt; [I use <a href="http://rvm.beginrescueend.com/">RVM</a> to switch ruby between different version]
* Bowline gem -----------------------&gt; sudo gem install <a href="http://github.com/maccman/bowline">bowline</a>

<strong>RVM</strong>

* <a href="http://rvm.beginrescueend.com/rvm/install/">Install RVM</a> to manage Ruby easily, then you decide which version you will use.

OK, Now create an application in an easy way:
<span style="color: #0000ff;"><em>&gt;&gt; bowline-gen app helloworld
&gt;&gt; cd helloworld
&gt;&gt; bowline-bundle
&gt;&gt; ./script/run</em></span>

Unluckily, On Ubuntu 9.0.4, There is an error about a needed lib when I run the application, see
<span style="color: #0000ff;"><em>/usr/lib/libstdc++.so.6: version `GLIBCXX_3.4.11' not found (required by /home/andy/.bowline/bowline-desktop)</em></span>

I searched around and found it's something wrong with gcc version, or these is still a webkit lib involved issue under Ubuntu9.0.4, anyway, it's interesting to me, I am now wondering if we can reference some bowline experience to create iphone/ipad application based on ruby on rails. not sure, I am researching in advance.
