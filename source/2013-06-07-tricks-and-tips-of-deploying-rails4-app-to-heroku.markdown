---
layout: post
title: "Tricks and Tips of Deploying Rails4 App to Heroku"
date: 2013-06-07 23:01
comments: true
categories:
- rails4
- ruby2
- heroku
- deployment
- basic auth 
---
Recently, I deployed a client project to Heroku and made the Heroku instance as an internal demo server. The project is based on Ruby2.0 and Rails4, unexpectedly, the deployment to Heroku is not as smooth as before. Below I'd like to share some tricks and tips that I came across. 

##### Rails4 Specific Tricks

* Heroku forces you to specify your ruby version in Gemfile, it's supported by bundler from [1.2 version], so just add below line into your Gemfile:

{% codeblock ruby %}
# specify ruby version to enable the deploy to Heroku instance.
ruby '2.0.0'
{% endcodeblock %}

* Rails4 gets rid of plugin system. In order to use features such as static asset serving and logging on Heroku, you should add the following gems to your Gemfile:

```
gem 'rails_log_stdout',           github: 'Heroku/rails_log_stdout'
gem 'rails3_serve_static_assets', github: 'Heroku/rails3_serve_static_assets'
```

* Use [puma] as the web server, you want to add a `Procfile` file and add below line in it:

```
web: bundle exec puma -p $PORT
```

* Below http basic auth doesn't work as what I did before for non-rails4 app on Heroku.

```
config.middleware.insert_after(::Rack::Lock, "::Rack::Auth::Basic", "Production") do |u, p|
  [u, p] == [USER, PASSWORD]
end
```
```
# Error message when pushing to Heroku...
-----> Preparing app for Rails asset pipeline
       Running: rake assets:precompile
       rake aborted!
       No such middleware to insert after: Rack::Lock
```

* Actually, Rails4 is thread safe by default, you do not have the overhead of including the `Rack::Lock` middleware in each request. So just use `Rack::Auth::Basic` directly as there is no Rack::Lock middleware any more when you using a web server such as `puma`:

```
config.middleware.use '::Rack::Auth::Basic' do |u, p|
  [u, p] == [USER, PASSWORD]
end
```

##### Heroku Related Tips

In my case, I need to transfer PG database between local and Heroku. Firstly, I need to find the URL to my db on Heroku:

```
$ heroku config:get DATABASE_URL
postgres://bla:sth@ec2-17-21-12-11.compute-1.amazonaws.com:5432/123
```

Then transfer from the Heroku db to your local db (switch -t `to` and -f `from` versus):

```
$ heroku plugins:install https://github.com/ddollar/heroku-pg-transfer
$ heroku pg:transfer -t postgres://localhost/dbname -f postgres://bla:sth@ec2-17-21-12-11.compute-1.amazonaws.com:5432/123
```

Since the [heroku-pg-transfer] tool utilizes postgres's native pg_dump facility it is a much more predictable and resilient tool. Check out a related blog [for more details].

There is another needs in my case, I have to deploy `development` branch to Heroku, but Heroku default is to deploy master branch to their instance, use below command to specify a branch for deployment.

```
# deploy a specific branch to Heroku
git push heroku other-barnch:master
```

#### Resources
<https://devcenter.heroku.com/articles/rails4><br />
<http://blog.remarkablelabs.com/2012/12/rails-4-is-thread-safe-by-default-rails-4-countdown-to-2013><br />


[puma]: http://puma.io/
[1.2 version]: http://gembundler.com/v1.2/whats_new.html
[for more details]: http://www.ryandaigle.com/a/pgtransfer-is-the-new-taps
[heroku-pg-transfer]: https://github.com/ddollar/heroku-pg-transfer

