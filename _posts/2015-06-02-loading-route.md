---
layout: post
title: Loading Route for EmberJS
---
When building an ember application, it's nice to provide a global loading route
for when a route takes a long time to load. This is especially important if
you're using a library like `liquid-fire` for transitions between routes.

While it should always be a goal to optimize slow loading routes, it's not
always possible in all cases, especially for mobile users. For these cases, you
want to show a loading spinner, or loading animation of some sort. This lets
the user know that their request is being processed by your application.

Adding a global loading view is pretty straightforward. The first thing you'll
need to do is add a loading action to your application. You can do this in
`app/application/route.js`.

```
  import Ember from 'ember';

  export default Ember.Route.extend({
    actions: {
      loading() {
        const view = this.container.lookup('view:loading').append();
        this.router.one('didTransition', view, 'destroy');
      }
    }
  });
```

Once that's done, you'll need to create a view file.

`app/loading/view.js`

```
  import Ember from 'ember';

  export default Ember.View.extend({
    templateName: 'loading',
    elementId: 'global-loading'
  });
```

You can then add your template file, where you'll put the markup for your
loading spinner.

`app/loading/template.hbs`

```
  <div class="loading">Loading&#8230;</div>
```
