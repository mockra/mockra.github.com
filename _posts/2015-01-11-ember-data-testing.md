---
layout: post
title: Ember Data Testing
---
If you're looking to test your `ember-cli` application, and you're using Ember
Data, then you'll want to use mocks instead of fixtures. Luckily, `ember-cli`
provides a decent tool set for creating mock server responses.

You can generate a new endpoint mock by running:

`ember g http-mock resource-name`

You would replace `resource-name` with something like `users` or `posts`.

One of the main downsides to this approach is that we'll need to run `ember
serve` before running our tests, so that our mock expressjs server will serve
our response.

Once we have our server running, when we run our tests, `ember-data` will
receive the response we setup in our mock endpoint.
