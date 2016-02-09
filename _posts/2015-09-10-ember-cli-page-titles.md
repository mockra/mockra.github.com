---
layout: post
title: Ember Cli Page Titles
---
Adding page titles to your EmberJS routes is a great way to improve the user
experience. Like most things with EmberJS, there's an addon that makes it easy
to add page titles.

Here's a quick rundown of how to get started. You'll first need to install the
addon by running:

~~~
  ember install ember-cli-document-title
~~~

You can then add static page titles to routes with the following code:

~~~
  // post/route.js
  export default Ember.Route.extend({
    title: 'Our Favorite posts!'
  });
~~~

If you're looking for something a little more complex, you can add dynamic
routes with the following code:

~~~
  // fighter/route.js
  export default Ember.Route.extend({
    titleToken: function(model) {
      return get(model, 'name');
    }
  });
~~~

The real power comes when you combine the two, here's an example of a dynamic
route combined with a static application title.

~~~
  // application/route.js
  export default Ember.Route.extend({
    title: function(tokens) {
      if (tokens.length) {
        return 'My Website - ' + tokens.join(' - ');
      } else {
        return 'My Website - Thoughts and Musings';
      }
    }
  });
~~~
