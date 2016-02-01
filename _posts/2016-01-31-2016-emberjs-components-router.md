---
layout: post
title: Inject EmberJS Router into Components
---
If you find the need to change routes in a
component action, then you'll need access to the router. Here's a quick
example of an initializer that will inject the router into your components.

`app/initializers/component-routes.js`

```
  export function initialize(application) {
    application.inject('component', 'router', 'router:main')
  }

  export default {
    name: 'component-routes',
    initialize
  }
```

You can then access the router in your components like such:

```
  get(this, 'router').transitionTo('dashboard')
```
