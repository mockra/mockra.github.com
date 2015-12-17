---
layout: post
title: Babel Register with Node and Async
---
If you're looking to use [babel](https://babeljs.io/) with
[koa](http://koajs.com/), then here's a quick guide to get you started.

The first thing you'll need to do is install `babel-register`.

```
  npm install babel-register --save
```

You'll then want to setup a new entry file for your application. Here's an
example of using `index.js` to load `babel-register` and `app.js`.

```
  require('babel-register')
  require('./app.js')
```

You're now setup to use Babel features in your application. If you're using Koa
though, then you likely want access to async functions, which requires a little
more setup.

The first thing you'll need to do is install the async plugin:

```
  npm install babel-plugin-transform-async-to-generator --save
```

Once that's done, you'll need to setup a `.babelrc` file:

```
  {
    "plugins": ["transform-async-to-generator"]
  }
```

You can now take advantage of async functions in your application. Here's an
example of a logger that uses async.

```
  module.exports = (app) => {
    app.use(async (ctx, next) => {
      const start = new Date
      await next()
      const ms = new Date - start
      console.log(`${ctx.method} ${ctx.url} - ${ms} ms`)
    })

    return app
  }
```
