---
layout: post
title: Node - EmberJS Rest Serializer
---
[Node Rest Serializer](https://github.com/mockra/node-rest-serializer)

I recently created a module for serializing objects pulled from my database
for my JSON Api. I'm currently using the RestSerializer on a few of my
projects while waiting for more adoption around the JSON Api. I felt some pain
around manually serializing my objects in routes, so I decided to create a
library for handling the serialization.

When designing the API for my module, I wanted to keep the interface simple
and functional. My goal was to be able to do something simple like the
following in my node applications.

~~~
  ctx.body = serialize('users', users, {
    sideload: { name: 'posts' },
    without: ['password', 'token']
  })
~~~

I'll typically create a unique serializer for each type of document in my API,
which helps to keep my routes cleaner. A user serializer would give me the
option to do something like:

~~~
  ctx.body = userSerializer(users, { withPosts: true })
~~~

If you're interested in providing an API for the EmberJS RestSerializer, or
adding better serialization support in your Node apps, feel free to check out
the module, [here](https://github.com/mockra/node-rest-serializer).
