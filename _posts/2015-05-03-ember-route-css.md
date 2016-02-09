---
layout: post
title: EmberJS - Body Route CSS
---
There's a variety of reasons you might want to add a route specific tag to the
body element of your application, so it's nice to be able to provide that
functionality for your designer.

Here's an example of setting a body tag through an initializer. The first thing
you'll want to do is create an initializer file, such as
`app/initializers/route-body-tags.js`.

You can then insert the following code:

~~~
  import Ember from 'ember';

  var alreadyRun = false;

  export function initialize(/* container, application */) {
    if (alreadyRun) {
      return;
    } else {
      alreadyRun = true;
    }

    Ember.Route.reopen({
      activate: function() {
        var cssClass = this.toCssClass();
        if (cssClass != 'application') {
          Ember.$('body').addClass(cssClass);
        }
      },

      deactivate: function() {
        Ember.$('body').removeClass(this.toCssClass());
      },

      toCssClass: function() {
        return this.routeName.replace(/\./g, '-').dasherize();
      }
    });
  }

  export default {
    name: 'route-body-tags',
    initialize: initialize
  };
~~~
