---
layout: post
title: EmberJS Component Testing
---
Testing components in EmberJS is much more straight forward than you might
expect. Here's an example test for the [Gravtar
component](http://mockra.com/2014/08/17/emberjs-gravatar-component/) I wrote a
post about.

{% gist mockra/7af2d94cee1e571a00b8 %}

In this test, we're setting up our component inside an `Ember.run` block, so
that the setup happens before we run our tests. After the setup, we're
appending our rendered component to the DOM by calling `this.append();`.

Once the component is added to the DOM, we can use our selector methods to
ensure that the image source has been correctly set by our component.
