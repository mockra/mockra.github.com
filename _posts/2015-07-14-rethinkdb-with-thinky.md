---
layout: post
title: Using RethinkDB with Thinky
---
I've been messing around with RethinkDB, and I've been impressed with what
I've seen so far. It provides a lot of the same benefits as MongoDB, but adds
a lot of additional functionality, and supposedly makes scaling a breeze. The
administrator feature is a great nice to have as well.

I've been using the [Thinky](https://thinky.io/) ORM to for interfacing with
RethinkDB, and it's suited my needs well so far. Here's a quick overview of
how I incorporate Thinky with my node projects.

The first thing I do is setup a `thinky.js` file that I can include in my
models.

```
  var config = require('../config');

  var thinky = require('thinky')(config.thinky);

  module.exports = thinky;
```

That `config.js` file looks like:

```
  module.exports = {
    thinky: {
      host: "localhost",
      port: 28015,
      authKey: "",
      db: "appName"
    }
  }
```

I can then include `thinky` in my models without reloading the `thinky` module.

```
  var thinky = require('../util/thinky.js');
  var type = thinky.type;

  var Post = thinky.createModel("Post", {
    id: type.string(),
    title: type.string()
  });

  module.exports = Post;
```
