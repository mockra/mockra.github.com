---
layout: post
title: Node Advanced Rest Serialization
---
In a previous blog post, I introduced a serializer library I created for use in
my JSON APIs. You can find that post,
[here](http://mockra.com/2016/01/28/node-emberjs-rest-serializer/).

In this post, I'm going to show an example of how I use this library in my
actual applications. The first step I take is creating a serializer for a
specific type of object. For this example, I'm going to show a user serializer.

~~~
  var serialize = require('rest-serializer')
  var _ = require('lodash')

  module.exports = function (data, args) {
    var key = ((_.isArray(data)) ? 'users' : 'user')
    var without = ['token', 'password', 'passwordConfirmation']
    var options = { without: without }

    args = args || {}
    if (args.withPosts) options.sideload = { name: 'posts' }

    return serialize(key, data, options)
  }
~~~

This serializer handles a few different things for us. The first thing it does
is set the correct key based on if we're serializing multiple users, or a
single user. The second thing it does is exclude three values from our records,
since we don't want to expose tokens or passwords in our API. The final thing
is does is accept the option to sideload post records.

We can then use this serializer in our route, like so:

~~~
  const User = require('../models/user')
  const serialize = require('../serializers/user')

  exports.index = async (ctx, next) => {
    const users = await User.filter({firstName: 'Mary'})
    ctx.body = serialize(users)
  }

  exports.show = async (ctx, next) => {
    const user = await User.get(ctx.params.id).getJoin({ posts: true })
    ctx.body = serialize(user, { withPosts: true })
  }
~~~

The serializer allows us to return an array of users in our index route without
including related posts. When we go to fetch a specific user, we pass in our
`withPosts` option to get the related post records. In both of these routes, we
don't need to worry about exposing sensitive data, because it's handled by the
serializer.
