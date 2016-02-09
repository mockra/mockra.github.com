---
layout: post
title: Importing Fonts with Ember-Cli
---
Most EmberJS applications are going to include multiple fonts, or other assets
that need to be imported. While this might seem daunting at first, there's an
easy way to include an entire directory without needing to specify each file
individually.

You'll need to first install `broccoli-static-compiler` with the following
command:

~~~
  npm install --save-dev broccoli-static-compiler
~~~

Here's an example `ember-cli-build.js` file that imports multiple fonts at
once.

~~~
  var EmberApp = require('ember-cli/lib/broccoli/ember-app');
  var pickFiles = require('broccoli-static-compiler');

  module.exports = function(defaults) {
    var app = new EmberApp(defaults, {
      fingerprint: {
        exclude: ['assets/emoji']
      }
    });

    app.import('bower_components/lodash/lodash.js');
    app.import('bower_components/moment/moment.js');

    var materializeFonts = pickFiles('bower_components/materialize/font/roboto', {
      srcDir: '/',
      destDir: '/font/roboto'
    });

    return app.toTree([materializeFonts]);
  };
~~~

The lines used to important the fonts are:

~~~
  var pickFiles = require('broccoli-static-compiler');

  var materializeFonts = pickFiles('bower_components/materialize/font/roboto', {
    srcDir: '/',
    destDir: '/font/roboto'
  });

  return app.toTree([materializeFonts]);
~~~
