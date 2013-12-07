--- 
layout: post
title: "valuable ruby on rails materials"
comments: true
categories: 
- "2010"
- ror
- Ruby On Rails
- training
- xdite
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
一直关注<a href="http://blog.xdite.net/">XDite的blog</a>，他写的关于Rails的文章总是能让我从中受益。看见他写的Ruby on Rails的入门书单与练习作业，感觉非常的精炼，这个post很适合当作Rails新手的入门指导，鉴于此，我也把它推荐给Team，用来培训新入职的Rails developer. 在这里谢谢XDite老师 :)

以下为全文转载，<a href="http://blog.xdite.net/?p=1754&amp;utm_source=feedburner&amp;utm_medium=feed&amp;utm_campaign=Feed%3A+xxddite+(Blog.XDite.net)">原文链接请点击此处</a>。

==================================================

學習 Ruby on Rails 最快的途徑無非是直接使用 Rails 撰寫產品。而這個過程中若有 mentor 指導以及 code review，學習進度也會加速不少。

但現實生活中並非如此理想，

第一，並不是每個人都有每天必須要以 Rails 撰寫產品的壓力（not a Rails Developer）。

第二，沒有循序漸進的入門途徑以及沒有 mentor。（Framework 進展太快，導致現有書籍版本跟不上進度，另外具有經驗的 mentor 太少，有的話也沒興趣回答過於初階的問題）

最近幾個月都在訓練 Rails Developer，零碎的東西講了不少遍。懶得一次次重講基礎的東西和開訓練菜單，乾脆整理成文字，以後新人就直接看這篇…

新人需要具備的「一般」基礎技能：
<ol>
	<li>對 Git 的觀念與技巧掌握。</li>
	<li>對 VIM / Textmate 的基本開發技巧掌握。</li>
	<li>熟悉 Linux Command Line 的操作。</li>
</ol>
* Git

書單

Peepcode 的 <a href="http://peepcode.com/products/git" target="_blank">Git</a> 與 <a href="http://progit.org/book/" target="_blank">Pro Git</a>

練習

上 Github 開啟一個專案，練習 git commit , git push , git pull, git branch , git checkout , git merge

* Editor

書單

c9s 的 <a href="http://c9s.blogspot.com/2009/08/vim-hacks-coscup.html" target="_blank">VIM Hacks</a> 與 Oreilly 的 <a href="http://tlsj.tenlong.com.tw/WebModule/BookSearch/bookSearchViewAction.do?isbn=9789866840326&amp;sid=48676&amp;aid=69e42ffb" target="_blank">精通 vi 與 vim</a> 與 Pragmatic 的 <a href="http://www.pragprog.com/titles/textmate/textmate" target="_blank">TextMate: Power Editing for the Mac</a>

練習

vgod 的 <a href="http://blog.vgod.tw/2009/12/08/vim-cheat-sheet-for-programmers/" target="_blank">給程式設計師的Vim入門圖解說明</a> 全部練習一遍

* Linux CLI

書單與練習：

Peepcode 的 <a href="http://peepcode.com/products/meet-the-command-line" target="_blank">Meet the Command Line</a> 、<a href="http://peepcode.com/products/advanced-command-line" target="_blank">Advanced Command Line </a> 全部練過一遍

=====

新人需要具備的 Rails 基礎技能：
<ol>
	<li>可手刻 CRUD ( Create / Read / Update / Delete ) 並且理解 CRUD 中的 params 傳遞方法</li>
	<li>route 中 resources 觀念配合 model 裡 has_many 的設計，理解並熟悉 RESTful 觀念。</li>
	<li>route 的優先順序與 routes 中 resource / namespace 的實作。</li>
	<li>named_scope 、 counter_cache、before_filter</li>
	<li>plugin 的使用：<a href="http://github.com/technoweenie/restful-authentication" target="_blank">restful-authentication</a>、<a href="http://wiki.github.com/mislav/will_paginate/" target="_blank">will_paginate</a>、<a href="http://github.com/thoughtbot/paperclip" target="_blank">paperclip</a></li>
	<li>rake 原理以及撰寫 task</li>
	<li>ruby on rails 的 production setup 與撰寫 <a href="http://www.capify.org/" target="_blank">capistrano</a> recipes</li>
</ol>
書單：（案頭必備）

<a href="http://www.books.com.tw/exep/prod/booksfile.php?item=0010350699" target="_blank">Ruby Programming — 向 Ruby 之父學程式設計</a>
<a href="http://www.books.com.tw/exep/prod/booksfile.php?item=0010400655" target="_blank">Ruby for Rails - Rails 開發者必備的 Ruby 學習手冊</a> （英文新版： <a href="http://www.manning.com/black2/" target="_blank">The Well-Grounded Rubyist</a> )
<a href="http://www.books.com.tw/exep/prod/booksfile.php?item=0010374225" target="_blank">碼上就會：Rails敏捷開發網站</a> （英文新版: <a href="http://www.pragprog.com/titles/rails3/agile-web-development-with-rails-third-edition" target="_blank">Agile Web Development with Rails, Third Edition</a> )
<a href="http://my.safaribooksonline.com/9780321445612" target="_blank">The Rails Way</a>
<a href="http://oreilly.com/catalog/9780596514815" target="_blank">Ruby Pocket Reference</a>
<a href="http://www.pragprog.com/titles/fr_rr/rails-recipes" target="_blank">Rails Recipes</a>
<a href="http://www.pragprog.com/titles/fr_arr/advanced-rails-recipes" target="_blank">Advanced Rails Recipes: 84 New Ways to Build Stunning Rails Apps</a>

線上工具：（必加書籤）

Ruby API : <a href="http://www.ruby-doc.org/core/classes/String.html" target="_blank">String</a>、<a href="http://www.ruby-doc.org/core/classes/Array.html" target="_blank">Array</a>、<a href="http://www.ruby-doc.org/core/classes/Hash.html" target="_blank">Hash</a>
APIDock : <a href="http://apidock.com/rails" target="_blank">Ruby on Rails</a>

練習作業：

（1）開發一個簡易論壇系統。系統要有 Forum 與 Post 兩個 model，寫出 CRUD 介面，並且文章網址是使用 <a href="http://example.org/forum/1/post/2" target="_blank">http://example.org/forum/1/post/2</a> 這種表示。

吸收觀念：

* CRUD &amp; migration
* has_many 與 belongs_to
* resources 與雙層 resources
* before_filter : find_event

參考資料：

* <a href="http://rails.pixnet.net/blog/post/22956704" target="_blank">深入淺出 RoR (4-3) - RESTful 與 CRUD action</a>
* <a href="http://ihower.tw/training/rails-tutoral.html" target="_blank">ihower training : Ruby on Rails 入門</a>

( 2）使用者必須能夠 註冊 / 登入，登入後才可以發表 Post，不然只能瀏覽。只有自己的 Post 才能進行修改與刪除。

吸收觀念：

* routes 優先權與 route alias
* plugin 安裝與使用
* before_filter : login_required
* session : current_user
* <a href="http://api.rubyonrails.org/classes/ActiveRecord/Base.html#M002281" target="_blank">attr_accessible</a> / <a href="http://api.rubyonrails.org/classes/ActiveRecord/Base.html#M002280" target="_blank">attr_protected</a>

參考資料：

* <a href="http://github.com/technoweenie/restful-authentication" target="_blank">restful-authentication</a>

( 3）論壇的文章要能夠分頁，每一頁 20 筆，每一個論壇要秀出現在論壇裡有多少 post 數量。可用 params 配合 named_scope 在文章列表排序。

吸收觀念：

* pagination
* counter_cache
* named_scope :recent

參考資料：

* <a href="http://wiki.github.com/mislav/will_paginate/" target="_blank">will_paginate</a>
* <a href="http://railscasts.com/episodes/23-counter-cache-column" target="_blank">Railscast : Counter Cache Column</a>
* <a href="http://railscasts.com/episodes/108-named-scope" target="_blank">Railscast : named_scope</a>

( 4）每篇文章可以上傳附件

吸收觀念：

* form_for  multipart

參考資料：

* <a href="http://github.com/thoughtbot/paperclip" target="_blank">paperclip</a>

( 5）Admin 可以刪改所有文章，建立一個後台做這件事。網址是 <a href="http://example.org/admin/" target="_blank">http://example.org/admin/</a>。只有身分是 admin 的人可以進後台。admin 的判別方是 column 裡加一個 boolean，判斷是否 admin。這個 attribute 必須用 <a href="http://api.rubyonrails.org/classes/ActiveRecord/Base.html#M002281" target="_blank">attr_accessible</a> / <a href="http://api.rubyonrails.org/classes/ActiveRecord/Base.html#M002280" target="_blank">attr_protected</a> 保護。

吸收觀念：

* route : namespace
* before_filter : require_is_admin

參考資料：

* <a href="http://railstips.org/blog/archives/2007/04/28/namespaces-added-to-routes/" target="_blank">Namespaces added to routes</a>

( 6）用 Rake 撰寫自動化步驟，生假資料。寫一個 rake 可以達成以下步驟：「砍 db =&gt; 建 db =&gt; 跑 migration =&gt; 生種子資料」，另一個 rake 是生假文章與假論壇。

吸收觀念：

* rake -T
* rake db:drop ; rake db:create ; rake db:migrate ; rake db:seed
* rake dev:fake ( 自己寫 namespace : dev, 裡面放一個 task 叫做 fake，fake 資料用 <a href="http://github.com/ryanb/populator" target="_blank">Populator</a> 生）

參考資料：

* <a href="http://railsenvy.com/2007/6/11/ruby-on-rails-rake-tutorial" target="_blank">Ruby on Rails Rake Tutorial (aka. How rake turned me into an alcoholic)</a>
* <a href="http://ryandaigle.com/articles/2009/5/13/what-s-new-in-edge-rails-database-seeding" target="_blank">What’s New in Edge Rails: Database Seeding</a>

( 7）在租來的 VPS 上面建置 Ruby on Rails production 環境，使用 Ruby Enterprise 與 mod_rails。使用 capistrano 佈署 application。

吸收觀念：

* cap deploy:setup , cap deploy , cap deploy:rollback , cap deploy:restart

參考資料：

* <a href="http://github.com/jnstq/rails-nginx-passenger-ubuntu" target="_blank">rails-nginx-passenger-ubuntu </a>
* AWDR3 的 deploy 章節 , <a href="http://oreilly.com/catalog/9780596514815" target="_blank">Ruby Pocket Reference</a> 的 capistrano 章節

===

PS. 實際測試的結果是，完全不懂 Ruby on Rails 的新人，從頭帶過大概兩週可以練完這一份作業。
