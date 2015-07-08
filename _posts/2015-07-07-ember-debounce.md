---
layout: post
title: Ember Debounce - Autocomplete
---
While it's nice to provide instant feedback to your user, there are times when
it's wise to slow things down for your back-end. An example of such a case is
an autocomplete field. While it would be nice to repopulate the results as
soon as the input changes, it's smart to add an artificial delay.

That's where the `Ember.run.debounce` function comes in handy. Instead of
immediately updating search results, we can wait until the user is done adding
to the input field. This isn't always the best user experience, but for some
features, the trade off is worthwhile.

Here's an example of implementing such a feature using `Ember.run.debounce`.

```
  import Ember from 'ember';
  const { get, set, observer } = Ember;

  export default Ember.Controller.extend({
    searchText: null,
    posts: [],

    setPosts() {
      const searchText = get(this, 'searchText');

      if (get(searchText, 'length')) {
        set(this, 'posts', this.store.find('post', {title: searchText}));
      }
    },

    watchSearchText: observer('searchText', function() {
      Ember.run.debounce(this, this.setPosts, 200);
    })
  });
```

And the template:

```
{% raw %}
  <div class="list-group">
    {{#each posts key="id" as |post|}}
      <h4 class="list-group-item-heading">{{post.title}}</h4>
      <p class="list-group-item-text">{{post.content}}</p>
    {{/each}}
  </div>
{% endraw %}
```
