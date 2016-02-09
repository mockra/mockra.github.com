---
layout: post
title: Local Time for Rails
---
Dealing with timezones is one of the more painful parts of the development
process on most stacks. Luckily due to a variety of available tools and strong
conventions provided by Ruby on Rails, timezones are much easier to wrangle.

One of my favorite tools for providing dates in a user's given timezone is the
`local_time` gem. You can find the documentation,
[here](https://github.com/basecamp/local_time).

To install the gem you'll first need to add it to your `Gemfile`.

`gem 'local_time'`

You can then run `bundle install`. Once that's done, you'll need to include the
provided javascript file in your `app/assets/javascripts/application.js`. You
can do so by adding the following line:

`//= require local_time`

You'll then use the helper methods provided to display your dates. Here's an
example:


~~~
  <%= local_time_ago(comment.created_at) %>
  # Output: 14 hours ago
~~~
