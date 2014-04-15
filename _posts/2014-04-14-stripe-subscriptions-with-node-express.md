---
layout: post
title: Stripe Subscriptions with Node/Express
---
Adding payment options to your web application is easier than ever. One of the
services that makes accepting payments so easy is
[Stripe](https://stripe.com/). Here's an example of setting up a subscription
service for a node application.

## Front End

The first step in adding Stripe integration to your application is adding a
subscription page with a form. Stripe provides detailed documentation for
setting up a form using their javascript library. You'll find those
instructions [here](https://stripe.com/docs/tutorials/forms).

You'll want to make sure you update the action of the form they've supplied to
the corresponding path on your server. The form for my subscription page looks
like: `form(method='POST' action="/subscriptions" id="payment-form")`.

## Server

If you've setup the subscription page correctly according to the Stripe
documentation, then setting up the corresponding logic on your server should be
easy.

You'll want to make sure you have a place in your `userSchema` to store the
Stripe customer token for your user. Here's an example:

{% gist 10690806 %}

We can then create the corresponding route and action to handle our new form.
We're going to use the official node library provided by Stripe to handle our
subscriptions. You can install the library with the following command: `npm
install stripe --save`.

Make sure you have a route setup to handle the form.

    var subscriptions = require('./controllers/subscriptions');
    app.post('/subscriptions', subscriptions.create);

On the server side, we want to tell Stripe to create a new user for a specific
plan, e-mail, and card token we've just received. You'll also want to
make sure you've setup a subscription plan through the Stripe dashboard. Keep
in mind that Stripe doesn't share plans between `test/production`, so you'll want
to setup one for both.

{% gist 10691359 %}

Make sure you provide your own secret API key and plan id. You'll also want to
handle saving your user and providing a response. You might also want to setup
Stripe to handle sending your customers a receipt, otherwise you'll have to
handle that on your end.
