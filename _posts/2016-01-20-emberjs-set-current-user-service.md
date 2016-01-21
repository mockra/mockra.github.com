---
layout: post
title: EmberJS - Set Current User Service
---
If you're using the ember simple auth addon for authentication, then you'll
likely want to setup a service for setting the current user. Here's an example
of overriding the session service to setup a `currentUser`.

```
  import Ember from 'ember';
  import SimpleSession from "ember-simple-auth/services/session";
  const { get, set, observer } = Ember;
  const { service } = Ember.inject;

  export default SimpleSession.extend({
    store: service(),

    setCurrentUser: observer('isAuthenticated', async function() {
      if (get(this, 'isAuthenticated')) {
        const user = await get(this, 'store').queryRecord('user', {});
        set(this, 'currentUser', user);
      }
    })
  });
```

The key pieces to notice are that we're extending the original
ember-simple-auth session service. We're also injecting the store service,
which lets us fetch our user through ember-data.

The actual logic we're adding to the session service is in the
`setCurrentUser` observer. This observer watches the `isAuthenticated`
property, and fetches the user based on the auth header.

Here's an example of accessing the `currentUser` through a component.

```
  import Ember from 'ember';
  const { service } = Ember.inject;

  export default Ember.Component.extend({
    session: service()
  });
```

Here's the template:

```
{% raw %}
  {{#if session.isAuthenticated}}
    {{session.currentUser.email}}
  {{/if}}
{% endraw %}
```
