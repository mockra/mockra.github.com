---
layout: post
title: Ember Validations
---
Forms designed around user experience need to have most of the validation done
on the client side. If you're using EmberJS, then
[ember-validations](https://github.com/dockyard/ember-validations) provides a
great solution to adding validation to your forms.

Once you've selected the build you want to use, you'll also need to import the
library. You can do so by adding the following line to your `Brocfile.js`. This
line might change depending on the location of your ember-validations folder.

`app.import('vendor/ember-validations/index.js');`

Here's an example of validation handling for a Sign Up form.

##Controller##

{% gist mockra/700b942026ef9fdf2c34 %}

In the controller we're setting up the validations for our fields. We're
requiring all three fields, as well as validating the e-mail based on format.

##Form##

{% gist mockra/12b234dbe23a273018d2 %}

This is an example of how you can display an error using a form-field
component.
