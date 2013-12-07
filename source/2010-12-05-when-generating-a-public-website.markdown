--- 
layout: post
title: when generating a public website
comments: true
categories: 
- git
- html
- http
- javascript
- jquery
- Programing
- technology
- test
- web
- Web Application
- Web2.0
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: public-website-concerns
---
To backup a great topic, I pasted the following content to reminder me the public website concerns, it's not a summary by myself, I picked them up from <a href="http://www.stackoverflow.com" target="_blank">stackoverflow.com</a>.

<strong>Interface and User Experience</strong>
<ul>
	<li>Be aware that browsers implement standards inconsistently and make sure your site works reasonably well across all major browsers. At a minimum test against a recent <a rel="nofollow" href="http://en.wikipedia.org/wiki/Gecko_%28layout_engine%29">Gecko</a> engine (<a rel="nofollow" href="http://firefox.com/">Firefox</a>), a Webkit engine (<a rel="nofollow" href="http://www.apple.com/safari/">Safari</a>, <a rel="nofollow" href="http://www.google.com/chrome">Chrome</a>, and some mobile browsers), your supported IE browsers (take advantage of the<a rel="nofollow" href="http://www.microsoft.com/Downloads/details.aspx?FamilyID=21eabb90-958f-4b64-b5f1-73d0a413c8ef&amp;displaylang=en">Application Compatibility VPC Images</a>), and <a rel="nofollow" href="http://www.opera.com/">Opera</a>. Also consider how <a rel="nofollow" href="http://www.browsershots.org/">browsers render your site</a> in different operating systems.</li>
	<li>Consider how people might use the site other than from the major browsers: cell phones, screen readers and search engines, for example. — Some accessibility info: <a rel="nofollow" href="http://www.w3.org/WAI/">WAI</a> and <a rel="nofollow" href="http://www.section508.gov/">Section508</a>, Mobile development:<a rel="nofollow" href="http://mobiforge.com/">MobiForge</a></li>
	<li>Staging: How to deploy updates without affecting your users. <a href="http://stackoverflow.com/questions/72394/what-should-a-developer-know-before-building-a-public-web-site#73970">Ed Lucas's answer</a> has some comments on this.</li>
	<li>Don't display unfriendly errors directly to the user</li>
	<li>Don't put users' email addresses in plain text as they will get spammed to death</li>
	<li><a rel="nofollow" href="http://www.codinghorror.com/blog/archives/001228.html">Build well-considered limits into your site</a> - This also belongs under Security.</li>
	<li>Learn how to do <a rel="nofollow" href="http://en.wikipedia.org/wiki/Progressive_enhancement">progressive enhancement</a></li>
	<li>Always <a rel="nofollow" href="http://en.wikipedia.org/wiki/Post/Redirect/Get">redirect after a POST</a>.</li>
	<li>Don't forget to take accessibility into account. It's always a good idea and in certain circumstances it's a <a rel="nofollow" href="http://www.section508.gov/">legal requirement</a>. <a rel="nofollow" href="http://www.w3.org/WAI/intro/aria">WAI-ARIA</a> is a good resource in this area.</li>
</ul>
<strong>Security</strong>
<ul>
	<li>It's a lot to digest but the <a rel="nofollow" href="http://www.owasp.org/index.php/Category%3aOWASP_Guide_Project">OWASP development guide</a> covers Web Site security from top to bottom</li>
	<li>Know about <a rel="nofollow" href="http://en.wikipedia.org/wiki/SQL_injection">SQL injection</a> and how to prevent it</li>
	<li>Never trust user input (cookies are user input too!)</li>
	<li><span style="text-decoration: line-through;">Encrypt</span> Hash and salt passwords rather than storing them plain-text.</li>
	<li>Don't try to come up with your own fancy authentication system: it's such an easy thing to get wrong in subtle and untestable ways and you wouldn't even know it until <em>after</em> you're hacked.</li>
	<li>Know the <a rel="nofollow" href="https://www.pcisecuritystandards.org/">rules for processing credit cards</a>. (<a href="http://stackoverflow.com/questions/51094/payment-processors-what-do-i-need-to-know-if-i-want-to-accept-credit-cards-on-m">See this question as well</a>)</li>
	<li>Use <a rel="nofollow" href="http://www.mozilla.org/projects/security/pki/nss/ssl/draft302.txt">SSL</a>/<a rel="nofollow" href="http://en.wikipedia.org/wiki/Https">HTTPS</a> for login and any pages where sensitive data is entered (like credit card info)</li>
	<li>How to resist session hijacking</li>
	<li>Avoid <a rel="nofollow" href="http://en.wikipedia.org/wiki/Cross-site_scripting">cross site scripting</a> (XSS)</li>
	<li>Avoid <a rel="nofollow" href="http://en.wikipedia.org/wiki/Cross-site_request_forgery">cross site request forgeries</a> (XSRF)</li>
	<li>Keep your system(s) up to date with the latest patches</li>
	<li>Make sure your database connection information is secured.</li>
	<li>Keep yourself informed about the latest attack techniques and vulnerabilities affecting your platform.</li>
	<li>Read <a rel="nofollow" href="http://code.google.com/p/browsersec/wiki/Main">The Google Browser Security Handbook</a></li>
	<li>Read <a rel="nofollow" href="http://amzn.com/0470170778">The Web Application Hackers Handbook</a></li>
</ul>
<strong>Performance</strong>
<ul>
	<li>Implement caching if necessary, understand and use <a rel="nofollow" href="http://www.mnot.net/cache_docs/">HTTP caching</a> properly as well as <a rel="nofollow" href="http://www.w3.org/TR/html5/offline.html">HTML5 Manifest</a></li>
	<li>Optimize images - don't use a 20 KB image for a repeating background</li>
	<li>Learn how to <a title="gzip content" rel="nofollow" href="http://developer.yahoo.com/performance/rules.html#gzip">gzip/deflate content</a> (<a href="http://stackoverflow.com/questions/1574168/gzip-vs-deflate-zlib-revisited">deflate is better</a>)</li>
	<li>Combine/concatenate multiple stylesheets or multiple script files to reduce number of browser connections and improve gzip ability to compress duplications between files</li>
	<li>Take a look at the <a rel="nofollow" href="http://developer.yahoo.com/performance/">Yahoo Exceptional Performance</a> site, lots of great guidelines including improving front-end performance and their <a rel="nofollow" href="http://developer.yahoo.com/yslow/">YSlow</a> tool. <a rel="nofollow" href="http://code.google.com/speed/page-speed/docs/rules_intro.html">Google page speed</a> is another tool for performance profiling. Both require<a rel="nofollow" href="http://getfirebug.com/">Firebug</a> installed.</li>
	<li>Use <a rel="nofollow" href="http://alistapart.com/articles/sprites">CSS Image Sprites</a> for small related images like toolbars (see the "minimize http requests" point)</li>
	<li>Busy web sites should consider <a rel="nofollow" href="http://developer.yahoo.com/performance/rules.html#split">splitting components across domains</a>. Specifically...</li>
	<li>Static content (ie, images, CSS, JavaScript, and generally content that doesn't need access to cookies) should go in a separate domain <em><a rel="nofollow" href="http://blog.stackoverflow.com/2009/08/a-few-speed-improvements/">that does not use cookies</a></em>, because all cookies for a domain and it's subdomains are sent with every request to the domain and its subdomains. One good option here is to use a Content Delivery Network (CDN).</li>
	<li>Minimize the total number of HTTP requests required for a browser to render the page.</li>
	<li>Utilize <a rel="nofollow" href="http://code.google.com/closure/compiler/">Google Closure Compiler</a> for JavaScript and <a rel="nofollow" href="http://developer.yahoo.com/yui/compressor/">other minification tools</a></li>
	<li>Make sure there’s a <code>favicon.ico</code> file in the root of the site, i.e. <code>/favicon.ico</code>. <a rel="nofollow" href="http://mathiasbynens.be/notes/rel-shortcut-icon">Browsers will automatically request it</a>, even if the icon isn’t mentioned in the HTML at all. If you don’t have a <code>/favicon.ico</code>, this will result in a lot of 404s, draining your server’s bandwidth.</li>
</ul>
<strong>SEO (Search Engine Optimization)</strong>
<ul>
	<li>Use "search engine friendly" URL's, i.e. use <code>example.com/pages/45-article-title</code> instead of<code>example.com/index.php?page=45</code></li>
	<li>Don't use links that say "click here". You're wasting an SEO opportunity and it makes things harder for people with screen readers.</li>
	<li>Have an <a rel="nofollow" href="http://www.sitemaps.org/">XML sitemap</a>, preferably in the default location <code>/sitemap.xml</code>.</li>
	<li>Use <a rel="nofollow" href="http://googlewebmastercentral.blogspot.com/2009/02/specify-your-canonical.html"><code>&lt;link rel="canonical" ... /&gt;</code></a> when you have multiple URLs that point to the same content</li>
	<li>Use <a rel="nofollow" href="http://www.google.com/webmasters/">Google Webmaster Tools</a> and <a rel="nofollow" href="http://siteexplorer.search.yahoo.com/">Yahoo Site Explorer</a></li>
	<li>Install <a rel="nofollow" href="http://www.google.com/analytics/">Google Analytics</a> right at the start (or an open source analysis tool like <a rel="nofollow" href="http://piwik.org/">Piwik</a>)</li>
	<li>Know how <a rel="nofollow" href="http://en.wikipedia.org/wiki/Robots_exclusion_standard">robots.txt</a> and search engine spiders work</li>
	<li>Redirect requests (using <code>301 Moved Permanently</code>) asking for <code>www.example.com</code> to <code>example.com</code> (or the other way round) to prevent splitting the google ranking between both sites</li>
	<li>Know that there can be bad behaving spiders out there</li>
	<li>If you have non-text content look into Google's sitemap extensions for video, etc. There is some good information about this in <a href="http://stackoverflow.com/questions/72394/what-should-a-developer-know-before-building-a-public-web-site#167608">Tim Farley's answer</a>.</li>
</ul>
<strong>Technology</strong>
<ul>
	<li>Understand <a rel="nofollow" href="http://www.ietf.org/rfc/rfc2616.txt">HTTP</a> and things like GET, POST, sessions, cookies, and what it means to be "stateless".</li>
	<li>Write your <a rel="nofollow" href="http://www.w3.org/TR/xhtml1/">XHTML</a>/<a rel="nofollow" href="http://www.w3.org/TR/REC-html40/">HTML</a> and <a rel="nofollow" href="http://www.w3.org/TR/CSS2/">CSS</a> according to the <a rel="nofollow" href="http://www.w3.org/TR/">W3C specifications</a> and make sure they <a rel="nofollow" href="http://validator.w3.org/">validate</a>. The goal here is to avoid browser quirks modes and as a bonus make it much easier to work with non-standard browsers like screen readers and mobile devices.</li>
	<li>Understand how JavaScript is processed in the browser.</li>
	<li>Understand how JavaScript, style sheets, and other resources used by your page are loaded and consider their impact on <em>perceived</em> performance. It may be appropriate in some cases to <a rel="nofollow" href="http://developer.yahoo.net/blog/archives/2007/07/high_performanc_5.html">move scripts to the bottom</a>of your pages.</li>
	<li>Understand how the JavaScript sandbox works, especially if you intend to use iframes.</li>
	<li>Be aware that JavaScript can and will be disabled, and that Ajax is therefore an extension not a baseline. Even if most normal users leave it on now, remember that NoScript is becoming more popular, mobile devices may not work as expected, and Google won't run most of your JavaScript when indexing the site.</li>
	<li>Learn the <a rel="nofollow" href="http://www.bigoakinc.com/blog/when-to-use-a-301-vs-302-redirect/">difference between 301 and 302 redirects</a> (this is also an SEO issue).</li>
	<li>Learn as much as you possibly can about your deployment platform</li>
	<li>Consider using a <a href="http://stackoverflow.com/questions/167531/is-it-ok-to-use-a-css-reset-stylesheet">Reset Style Sheet</a></li>
	<li>Consider JavaScript frameworks (such as <a rel="nofollow" href="http://jquery.com/">jQuery</a>, <a rel="nofollow" href="http://mootools.net/">MooTools</a>, or <a rel="nofollow" href="http://www.prototypejs.org/">Prototype</a>), which will hide a lot of the browser differences when using JavaScript for DOM manipulation</li>
</ul>
<strong>Bug fixing</strong>
<ul>
	<li>Understand you'll spend 20% of the time coding and 80% of it maintaining, so code accordingly</li>
	<li>Set up a good error reporting solution</li>
	<li>Have some system for people to contact you with suggestions and criticism.</li>
	<li>Document how the application works for future support staff and people performing maintenance</li>
	<li>Make frequent backups! (And make sure those backups are functional) <a href="http://stackoverflow.com/questions/72394/what-should-a-developer-know-before-building-a-public-web-site#73970">Ed Lucas's answer</a> has some advice. Have a Restore strategy, not just a Backup strategy.</li>
	<li>Use a version control system to store your files, such as <a rel="nofollow" href="http://subversion.apache.org/">Subversion</a> or <a rel="nofollow" href="http://git-scm.org/">Git</a></li>
	<li>Don't forget to do your Unit Testing. Frameworks like <a rel="nofollow" href="http://seleniumhq.org/">Selenium</a> can help.</li>
</ul>
Lots of stuff omitted not necessarily because they're not useful answers, but because they're either too detailed, out of scope, or go a bit too far for someone looking to get an overview of the things they should know. If you're one of those people you can read the rest of the answers to get more detailed information about the things mentioned in this list. If I get the time I'll add links to the various answers that contain the things mentioned in this list if the answers go into detail about these things. Please feel free to edit this as well, I probably missed some stuff or made some mistakes.

Check out its original post thread at <a href="http://stackoverflow.com/questions/72394" target="_blank">http://stackoverflow.com/questions/72394</a>
