---
layout: post
title: EmberJS Component Class Bindings
---
Here's a quick post on using one of ember's lesser known component features.
While recently working on the game of life in ember, I was able to create a
cell component without a template.

This was accomplished by using `classNameBindings`, and a `click` event
handler.

~~~
  import Ember from 'ember';
  const { get, set, computed } = Ember;
  const { alias } = computed;

  export default Ember.Component.extend({
    tagName: 'span',
    classNames: ['cell'],
    classNameBindings: ['alive'],
    alive: alias('cell.alive'),

    click() {
      set(this, 'alive', !get(this, 'alive'));
    }
  });
~~~

In this example, we're using a simple version of `classNameBindings` where
we're just passing in a property. When the `alive` property returns `true`, the
`alive` class is added. When that value is false, the cell component only has
the default `cell` class.

Another way we could have handled this using `classNameBindings` would be
passing in classes for both states.

~~~
  classNameBindings: ['alive:enabled:disabled']
~~~

In this example, we would add the `enabled` class for a truth value, and the
`disabled` class for a false value.
