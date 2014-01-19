---
layout: post
title: Ember Simple Auth
---
Adding authentication to your EmberJS application is pretty straight forward
if you use one of the existing libraries out there. My favorite auth library is
[ember-simple-auth](https://github.com/simplabs/ember-simple-auth).

Implementing ember-simple-auth is quick and easy, and it provides a pretty
robust auth implementation. The first step is adding an initializer for adding
ember-simple-auth to your application. You can do so with the following
command:

{% gist 8512368 %}

You'll also need to implement the route mixin provided by ember-simple-auth.
You can add this to your `router.js` file to do so.

{% gist 8512388 %}

In order to allow a user to login to your application, you'll need to create a
login route. The following gists will show you how to setup your login route
files.

{% gist 8512415 %}

{% gist 8512423 %}

{% gist 8512428 %}

Your back-end will also need to implement a `POST /token` API that returns an
`access_token`, as well as optional `expires_in` and `refresh_token` keys.

Here's an example implementation in Ruby on Rails:

{% gist 8512444 %}
