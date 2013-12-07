---
layout: post
title: "Run a Static Website on Heroku for Free"
date: 2012-10-22 20:00
comments: true
categories: 
- rack
- heroku
- wrapbootstrap
- ruby
---
<div class="thumbnail"><a href="http://wangyaodi.com"><img src="https://img.skitch.com/20121023-fxqkstawwd56ehbpecxq6ifkq8.preview.jpg" alt="Andy Wang - Professional Ruby on Rails Engineer, Senior Web Application Developer." /></a><br /><span>Uploaded with <a href="http://skitch.com">Skitch</a>!</span></div>

Recently, I plan to update my personal information on internet, I also plan to have a professional personal website on which I can show my introduction, skills and working experiences. I guess it will introduce me to the world in a cool way.

Well, first of all, I bought an awesome template on [wrapbootstrap], where all pretty templates are built on [Twitter's BootStrap], I guess everyone loves BootStrap, who doesn't?

Once I get the simple static HTML template for website, I am going to deploy it to Heroku for free. We know [Heroku] deliveries their popular cloud hosting for [Ruby on Rails], [Node.js] and other framework. How does it work for static HTML website hosting?

I found that, we actually can build s simple Rack application to `run` the static website on heroku. But how? See below:

- Add `Gemfile` to require the `rack` gem for the website.

```
source 'http://rubygems.org'
gem 'rack'
```

- Add `config.ru` file in root folder of the website, this will enable the Rack handlings. 

```
$stdout.sync = true

use Rack::Static,
  :urls => ["/font-awesome", "/js", "/img", "/style"],
  :root => "."

run lambda { |env|
  [
    200,
    {
      'Content-Type'  => 'text/html',
      'Cache-Control' => 'public, max-age=86400'
    },
    File.open('index.html', File::RDONLY)
  ]
}
``` 
- Add `Procfile` in root folder to config the heroku web server and worker(if there is any).

```
web: bundle exec rackup -p $PORT
```

Ok, now it's ready to deploy the whole website to Heroku, [here](https://devcenter.heroku.com/articles/git) is a detailed document that can help you to deploy a codebase to Heroku. Meanwhile, you are allow to customize your domain for any app running on Heroku, [here](https://devcenter.heroku.com/articles/custom-domains) is also a docment for this purpose on heroku help center.

Easy, right? I've run my awesome personal website on [wangyaodi.com](wangyaodi.com) according to above steps, give it a look if you are interested in it. You are also welcomed to fork its [source code](https://github.com/yorzi/cv-andywang) on github. Enjoy it!


[wrapbootstrap]: https://wrapbootstrap.com/
[Twitter's BootStrap]: http://twitter.github.com/bootstrap/
[Heroku]: http://heroku.com
[Ruby on Rails]: http://rubyonrails.org/
[Node.js]: http://nodejs.org/
