---
layout: post
title: Testing with ExpressJS
---
Testing with ExpressJS can be a bit tricky if you're coming from a Rails
background, but it's much easier than you might expect.

Here's an example controller test:

{% gist mockra/60825fe236417d162116 %}

The important things to notice are that we're using `supertest` to test our
API, which provides us with a way to test our API. We're also calling `done()`
once each of our specs are finished.

You can view the complete setup [here](https://github.com/Nytrick/esports-back).
