---
layout: post
title: Rails Formulaic - Form Testing
---
If you're already using factory girl and want to clean up your test suite, then
the [Formulaic](https://github.com/thoughtbot/formulaic) gem is a great option.
It allows you to pass in a hash of attributes to fill out a form.

Here's an example:

~~~
  fill_form_and_submit(:user, :new, attributes_for(:user))
~~~
