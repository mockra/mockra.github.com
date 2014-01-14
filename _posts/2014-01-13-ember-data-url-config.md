---
layout: post
title: Ember Data URL/Host
---
If you're looking to set a custom host for ember-data, you can do so when
setting up your adapter. Depending on the version of ember-data you're using,
you'll need to pass a `host` or `url` option.

{% gist 8413723 %}

Depending on the back-end you're using, you'll need to add support for cross
origin resource sharing. Rails users can use the
[rack-cors](https://github.com/cyu/rack-cors) library. The
[node-cors](https://github.com/troygoode/node-cors/) package looks promising
for express users.
