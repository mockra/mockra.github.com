---
layout: post
title: EmberJS Gravatar Component
---
Adding Gravatar support to an ember application is pretty straightforward, but
you will need to include a library that provides MD5 hashing support. The
library we're going to use in this example is
[JavaScript-MD5](https://github.com/blueimp/JavaScript-MD5). This example also
assumes you're using [ember-cli](http://mockra.com/2014/07/22/ember-cli/).

You'll first want to install the MD5 library with the following command:

`bower install --save JavaScript-MD5`

You can then include the library by adding the following line to `Brocfile.js`.

`app.import('bower_components/JavaScript-MD5/js/md5.js');`

Now that we've installed our library for generating an MD5 hash, we can create
our component. We'll want to generate the component using the command line
tools.

`ember generate component gravatar-image`

We can then update the generated component files to include the required code:

{% gist mockra/e40fcfc83882a7abd010 %}

{% gist mockra/deaf0cd01df0c10ca153 %}

You can then include a Gravatar image on your website with the following line:

{% gist mockra/3b52bf5f95e10771b98b %}
