---
layout: post
title: Node Tests with Mocha
---
Setting up testing for your node project can be a bit tricky due to a lack of
conventions around testing. Here's a simple example of setting up a test
environment for an `expressjs` application with `mocha`.

The first thing we'll want to do is install `mocha` and `chai` for our project.
We can do that with the following commands.

`npm install mocha --save-dev`

`npm install chai --save-dev`

Mocha is our test runner, and we'll be using chai to provide us with
expectations. It essentially gives us access to:

~~~
  expect([1, 2]).to.have.length(2)
~~~

Once we've finished installing the required libraries, we can add a test
script to our `package.json` file.

~~~
  "scripts": {
    "test": "find ./test -name '*_test.js' | xargs mocha -R spec"
  }
~~~

Now when we run `npm test`, we'll run every file in our test directory that
ends in `_test.js` through mocha.

In addition to adding a test command, we can setup a `mocha.opts` file in our
test directory to provide some sane defaults. Here's an example file:

~~~
--require ./test/common.js
--reporter spec
--ui bdd
--recursive
--colors
--timeout 60000
--slow 300
~~~

In this file, we're telling it to load the `common.js` file in our test
directory. We can then setup various globals and state in the `common.js` file
that will be required in each of our tests. If you're coming from a Ruby on
Rails background, think of it like `spec_helper.rb`.

Here's an example `common.js` file:

~~~
  global.chai = require('chai')
  global.expect = global.chai.expect
  global.app = require('../index')
  process.env.NODE_ENV = process.env.NODE_ENV || 'test';
  process.env.TEST_ENV = process.env.TEST_ENV || 'test';
~~~

In this file, we're setting up `expect`, `chai`, and `app` as global variables.
This prevents us from having to require `chai` and `chai.expect` in all of our
test files.

We're also setting the `NODE_ENV` and `TEST_ENV` to test. This allows us to
depend on the `NODE_ENV` when configuring our environment.

This basic setup can be expanded on to provide additional functionality, but
helps to provide a starting point for most node applications.
