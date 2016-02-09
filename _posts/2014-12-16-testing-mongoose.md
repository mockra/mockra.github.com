---
layout: post
title: Testing Mongoose
---
Including the database layer into my Node tests was one of the more daunting
tasks at first glance, but ended up being much simpler than I first expected.
I'm not thrilled with my approach, but it works, and has gotten me past the
hump of testing my node applications.

The first step is including my express `app` through a `common.js` file, which
you can read more about
[here](http://mockra.com/2014/12/09/node-tests-with-mocha/). This prevents
mongoose from generating an error by attempting to connect to the same mongo
instance multiple times. The downside is that we're loading our `app` for all
of our tests using `common.js`.

The next step is cleaning up after our tests, which I like to do
explicitly in each test file. This allows better awareness of the state you're
setting up in each test, as well as the performance impact. You can do so with
the following code:

~~~
  var Post = require('../../models/post'

  after(function(done) {
    Post.remove().exec()
    done()
  })
~~~

You will want to switch `Post` with whatever mongoose model you need to clean
up. This specific example will clear the `post` collection after all of the
tests in the block have run. This can be replaced with `afterEach` if you need
to clean up between each spec.
