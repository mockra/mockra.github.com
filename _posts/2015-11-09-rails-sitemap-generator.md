---
layout: post
title: Rails Sitemap Generator
---
If you're looking to add a sitemap for your rails application, I've found
[sitemap_generator](https://github.com/kjvarga/sitemap_generator) to be a great
tool. You can get started by adding the gem to your `Gemfile`.

```
  gem 'sitemap_generator'
```

You'll then need to create a `config/sitemap.rb` file that will be used to
generate your sitemap. You can generate this file by running:

```
  bundle exec rake sitemap:install
```

You'll then need to edit the `config/sitemap.rb` file, and add the routes you
want in your sitemap there. Here's an example:

```
  SitemapGenerator::Sitemap.default_host = "http://www.yourdomain.com"

  SitemapGenerator::Sitemap.create do
    Post.find_each do |post|
      add post_path(post)
    end
    add faq_path
  end
```

You can then run `rake sitemap:refresh` to generate a sitemap file for your
application. You'll also want to add the sitemap location to your `robots.txt`
file: `Sitemap: http://www.example.com/sitemap.xml.gz`

Depending on your server and deploy setup, you'll need to decide how to handle
refreshing and generating a production sitemap.

One option for refreshing your sitemap would be through `crontab`.

```
  every 1.day, :at => '5:00 am' do
    rake "-s sitemap:refresh"
  end
```

There's also built in support for hosting your sitemap on S3, which is useful
if you're behind a load balancer. Just make sure to update your `robots.txt`
with the correct location.
