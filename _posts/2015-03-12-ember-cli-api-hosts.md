---
layout: post
title: Ember-Cli API Hosts
---
If you have a typical server setup, then you likely need to specify your API
endpoint depending on environment. Setting up different hosts for your EmberJS
application can be done through the `config/enviornment.js` file.

~~~
 module.exports = function(environment) {
  if (environment === 'development') {
    ENV.API_HOST = "http://localhost:3000"
  }

  if (environment === 'production') {
    ENV.API_HOST = "https://yourapp.com"
  }
};
~~~

You can then setup your application adapter to use the correct endpoint through
the `app/adapters/application.js` file.

~~~
  import DS from 'ember-data';
  import config from "../config/environment";

  export default DS.ActiveModelAdapter.extend({
    namespace: 'api',
    host: config.API_HOST
  });
~~~
