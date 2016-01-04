---
layout: post
title: Convert Koa Middleware
---
If you're using Koa 2.0, you've likely noticed that a lot of middleware is no
longer compatible. Luckily, this is an easy fix, if not a bit ugly. If you
haven't run across this issue, then the error you'll see is:

```
TypeError: Support for generators has been removed. See the documentation for
examples of how to convert old middleware
https://github.com/koajs/koa#example-with-old-signature
```

This is generated because with 2.0 Koa removed support for generators, so
you'll need to convert your middleware to a supported format. In our case,
we're going to convert the old generator middleware to use promises. We'll do
so with the `koa-convert` library.

You can install `koa-convert` with:

```
  npm install koa-convert --save
```

Here's an example for converting old middleware using `koa-jade` and es6.

```
  const Koa = require('koa')
  const Jade = require('koa-jade')
  const convert = require('koa-convert')

  const app = new Koa()
  const jade = new Jade({
    viewPath: './views'
  })

  app.use(convert(jade.middleware))

  app.use(ctx => {
    ctx.render('index')
  })

  app.listen(3010)
```

The key lines we're using to convert the middleware are:

```
  const convert = require('koa-convert')

  app.use(convert(jade.middleware))
```

If your application relies on several old libraries, then you can just use
`convert` on each one.


```
  app.use(convert(jade.middleware))
  app.use(convert(serve('./views')))
```

Once you've converted all of your old generator middleware, you're good
to go!
