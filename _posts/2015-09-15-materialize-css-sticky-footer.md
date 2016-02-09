---
layout: post
title: MaterializeCSS Sticky Footer - EmberJS
---
I've been using the [MaterializeCSS](http://materializecss.com/) framework on
my latest side project ComboSumo.com. I've been pretty happy with it so far,
but I've had to use a few workarounds to support Safari.

If you've been using the sticky footer solution provided by the framework,
here's a quick example of how to get it to work with EmberJS, as well as the
Safari browser.

The key to getting it to work is applying the main flexbox rules to `body >
.ember-view` instead of the body tag. You'll also want to include additional
flexbox rules to support all of the browsers.

`app/application/template.hbs`

~~~
{% raw %}
  <main>
    {{outlet}}
  </main>

  {{footer-section}}
{% endraw %}
~~~

`app/components/footer-section/component.js`

~~~
  import Ember from 'ember';

  export default Ember.Component.extend({
    tagName: 'footer',
    classNames: ['page-footer']
  });
~~~

`app/styles/global.sass`

~~~
  body > .ember-view
    display: -webkit-box
    display: -webkit-flex
    display: -ms-flexbox
    display: flex
    min-height: 100vh
    -webkit-box-orient: vertical
    -webkit-box-direction: normal
    -webkit-flex-direction: column
    -ms-flex-direction: column
    flex-direction: column

  main
    -webkit-box-flex: 1
    -webkit-flex: 1 0 auto
    -ms-flex: 1 0 auto
    flex: 1 0 auto
~~~
