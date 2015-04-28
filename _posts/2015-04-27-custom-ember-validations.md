---
layout: post
title: Custom Ember Validations
---
A key component to any single page application is proper client side
validations. Providing the user instant feedback when they're filling out a
form is essential to a great user experience.

My favorite library for adding validations to an Ember application is
`ember-validations`. I mentioned the library in one of my previous blog
[posts](http://mockra.com/2014/09/15/ember-validations/).

While ember-validations provides a lot of build in validators, you'll
occasionally want to create a custom validation. Adding a custom validation
can be done by creating an appropriate file in the `app/validators` folder.

Here's an example of an e-mail validation.

`app/validators/local/email.js`

```
  import Ember from 'ember';
  import Base from 'ember-validations/validators/base';

  export default Base.extend({
    call: function() {
      if (!Ember.isEmpty(this.model.get(this.property))) {
        if (!/.+@.+\..{2,4}/.test(this.model.get(this.property))) {
          this.errors.pushObject("must be a valid e-mail address");
        }
      }
    }
  });
```

You can then use this validation in your controllers with the following syntax.

```
  email: {
    presence: true,
    email: true
  }
```
