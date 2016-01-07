---
layout: post
title: RethinkDB - Thinky Testing
---
If you're using thinky alongside mocha, then you'll likely want to reset the
database between each test. Here's a quick guide for performing the reset.

The first thing you'll want to do is a create a `test/helper.js` file.

```
  const config = require('../config')
  const thinky = require('../util/thinky')
  const _ = require('lodash')

  afterEach( async function (done) {
    const tables = await thinky.r.db(config.thinky.db).tableList()
    _.each(tables, async (table) => {
      await thinky.r.table(table).delete()
    })
    done()
  })
```

Depending on your application setup, you'll likely need to tweak the config
lines. `config.thinky.db` will need to be the name of your test database, such
as `your_app_test`.

You can then include this helper in your tests to include the reset
functionality.

```
  require('../helper')

  describe('User Model', function () {
  })
```

You can add additional setup to your `helper.js` file that you would like to
include in all your specs.
