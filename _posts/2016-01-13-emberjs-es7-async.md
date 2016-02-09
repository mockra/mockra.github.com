---
layout: post
title: EmberJS - ES7 Async/Await
---
Async functions are one of the more exciting features of ES7, and they can be
a great tool for cleaning up your EmberJS code. Here's a quick rundown on how
you can start using them in your application.

In your `ember-cli-build.js` file, you'll need to add a babel option:

~~~
  var app = new EmberApp(defaults, {
    babel: {
      includePolyfill: true
    }
  });
~~~

You can then start taking advantage of async/await in your app. Here's a quick
example of a component action:

~~~
  import Ember from 'ember';
  const { get, set } = Ember;
  const { service } = Ember.inject;

  export default Ember.Component.extend({
    store: service(),

    actions: {
      async register() {
        const user = get(this, 'store').createRecord('user', {
          email: get(this, 'email'),
          username: get(this, 'username'),
          password: get(this, 'password'),
          passwordConfirmation: get(this, 'passwordConfirmation')
        });

        try {
          await user.save();
          get(this, 'router').transitionTo('login');
        } catch(e) {
          set(this, 'error', true);
        }
      }
    }
  });
~~~
