---
layout: post
title: Ember Data Creating Records
keywords: [ember-data, emberjs]
---
Creating records with ember-data can be frustrating your first time around.
Without having a decent grasp on the framework, it can be hard to know the
server response you need to generate. This can be further escalated if you're
not sure why the response is failing.

The goal of this post is to present a guide to get you started, and hopefully
eliminate any unnecessary frustration. The controller action for creating
objects should look like:

{% gist mockra/61b706e673a6197eb817 %}

A few things to notice about this example. When submitting a form, we're
passing the `post` object to the `create` action. This lets us easily setup
that association when storing this `comment` record. When saving the record,
we're providing responses for both the success and failure scenarios.

When the comment is saved successfully, we're sending the user to the
`comments.show` route, and passing the new record as an argument. This will
allow us to stick the `comment.id` in the route path.

More importantly, in the case of a failure scenario, we're logging the error
message to the console. When persisting a record in EmberJS, a failure can be
caused by a variety of things. Something as simple as returning an associated
model in your server response that hasn't been defined as an `ember` model can
cause a failure. By logging the reason for the failure, we make it easier to
solve any bugs in our code.

The server response for the action would look like:

{% gist mockra/45e6457d14622a1c2272 %}

We'll also want to return a status code of `201`.

##Edit 11/02/2014##

If you're using async relationships, then you'll need to update to the latest
version of ember-data. You can find details in this issue:

https://github.com/emberjs/data/pull/1535
