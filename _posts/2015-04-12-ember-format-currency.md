---
layout: post
title: Formatting Currency in EmberJS
---
Most applications have a need to format currency for their users. Doing so
with an EmberJS application can be accomplished using components and
[AccountingJS](http://openexchangerates.github.io/accounting.js/).

To get started, you'll first need to install the AccountingJS library. You can
do so using bower with the following command:

~~~
  bower install accounting.js --save
~~~

You'll then need to import that library by adding the following line to
`Brocfile.js`. You might also want to update your `.jshintrc` file to reflect
that `accounting` will be predefined.

~~~
  app.import('bower_components/accounting.js/accounting.js');
~~~

You'll then want to generate your component, and add in the following code.

~~~
  import Ember from 'ember';

  export default Ember.Component.extend({
    value: 0,

    formattedValue: function() {
      return accounting.formatMoney(this.get('value'), {
        precision: 2
      });
    }.property('value')
  });
~~~

And the template:

~~~
{% raw %}
  {{formattedValue}}
{% endraw %}
~~~

You can then use the following component call when you need to format a
numeric value.

~~~
{% raw %}
  {{format-currency value=totalCost}}
{% endraw %}
~~~
