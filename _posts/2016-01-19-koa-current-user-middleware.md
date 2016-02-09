---
layout: post
title: Koa - Current User Middleware
---
Most applications on the web have some sort of authentication, and will want
to associate a current user with a request. Here's a quick example of adding
that functionality to Koa 2.0 using middleware.

Depending on your application, you will need to tweak a few lines to get it
working with your implementation. Notably, you'll need to adjust the token
pieces depending on how requests submit an authentication token to your
server.  You'll also need to adjust how you find or load a user based on your
ORM.

This example assumes the token is passed in a header that looks like:

~~~
  Token token="13p123p123n12pi3n1i31", email="test@example.com"
~~~

It also uses the Thinky ORM for RethinkDB. Here's an example of the middleware
that would go in: `middleware/current-user.js`

~~~
  const User = require('../models/user')

  module.exports = (app) => {
    app.use(async function (ctx, next) {
      // Get the Token from the Header
      const authHeader = ctx.request.header.authorization || ''
      const tokenParts = authHeader.match('token\=\"([a-z0-9]*)\"') || []
      const token = (tokenParts.length ? tokenParts[1] : null)

      if (token) {
        // Load the Current User
        const users = await User.filter({ token: token })
        const user = users[0]

        // Add the Current User to Request State
        ctx.state.currentUser = user
      }

      await next()
    })

    return app
  }
~~~

You can then include this middleware in your application by adding the
following line to `app.js` or `index.js`.

~~~
  require('./middleware/current-user')(app)
~~~

You can then access the current user in your routes with the following code:

~~~
  ctx.state.currentUser
~~~
