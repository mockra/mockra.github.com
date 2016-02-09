---
layout: post
title: Moment - Javascript Time Library
---
Working with dates in javascript doesn't have to be painful, the moment.js
library provides a great set of tools for working with time. If you're using
`NPM`, you can get started with the following command:

~~~
  npm install moment --save 
~~~

You'll then have access to a wide range of tools for formatting dates, as well
as manipulating time. Here's a few examples:

~~~
  moment().format('dddd');
  // Monday
  moment().add(2, 'days')
  // Wednesday
  moment().startOf('hour').fromNow();
  // An hour ago
~~~

You can add even more functionality in regards to dates, by also installing
`moment-range`.

~~~
  npm install moment-range --save
~~~

Moment-range allows you to work with time ranges, which can be useful for a
variety of problems.

Here's a couple of examples:

~~~
  moment().range(moment(), moment().add(14, 'days')).by('days', function(d) {
    console.log(d);
  });
~~~
