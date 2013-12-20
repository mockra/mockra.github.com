---
layout: post
title: Brunch, Express, and Ember.JS Guide - Part 1
---
This guide is going to be focused on building a back-end that works with the
[Ember.JS Getting Started tutorial](http://emberjs.com/guides/getting-started/).
The back-end we're going to build will utilize Express and Mongoose.
We'll also use Brunch and Bower to compile and manage our assets.

This first part of this guide will cover setting up our basic project
structure, and libraries. You can find the example application for this
tutorial on [Github](https://github.com/mockra/express_ember_example).

## Project Setup
Assuming you already have node.js installed, you'll need to install brunch and
bower.

    npm install -g brunch
    npm install -g bower

We're going to be using `brunch` to compile our assets, so that we can serve
them through our express application. `brunch` is similar to the asset pipeline
in Ruby on Rails applications.

If we want brunch to watch our `app` directory and automatically compile our
assets when we make changes, we'll need to run the following command.

    brunch watch

Bower will be used to download and manage our client-side libraries, such as
bootstrap, ember, and jquery.

### Generating our Project
The first step will be generating a basic brunch project. There are a
variety of Brunch skeletons available, but we're going to use a basic skeleton
for this project.

A skeleton in brunch is similar to a template; it provides a starting point for
your project. Some skeletons will create a project with Express, Ember, and
Bootstrap already setup.

    brunch new gh:brunch/dead-simple your-project-name
    cd your-project-name

### Downloading Ember
We now need to download ember and ember-data using bower. Since ember depends
on jquery and handlebars, bower automatically installs these libraries for us.

    bower install ember --save
    bower install ember-data-shim --save

We'll also need to install ember-handlebars for brunch, so brunch can correctly
compile our templates to work with ember.

    npm install ember-handlebars-brunch --save

The next step is to configure brunch to properly compile our assets into the
public directory. To do this, we need to tell brunch to look in the
bower_components directory. We can do this in `brunch-config.coffee`.

{% gist 8033792 %}

## Ember Setup

After we've installed our dependencies, we'll need to create a few files to get
Ember working. The first file is `app/initialize.js`, which will setup our
Ember application.

{% gist 8034261 %}

The second file we're going to create is `app/store.js`, which will configure
our RESTAdapter for Ember-Data. In this file we're setting a namespace, so we
can version our `express` api. We're also setting a custom primary key, so that
ember will work with MongoDB.

{% gist 8034269 %}

The final file is `app/router.js`. This includes the basic route you'll create
during the Ember.JS Tutorial.

{% gist 8034315 %}

## Express Setup

We now need to install the Express and Mongoose packages, so we can start
building out our back-end. Run the following commands to install these
libraries.

    npm install express --save
    npm install mongoose --save

An optional tool you can install is `node-dev`. `node-dev` is a development
tool that will restart your node process whenever you make changes to your
server files. You can install that tool with:

    npm install -g node-dev

Now that we have all of our dependencies installed, we can create our server
file, `server.js`.

{% gist 8050689 %}

You can run this file using `node-dev` by calling:

    node-dev server.js

You can then access your application at [0.0.0.0:3333](0.0.0.0:3333).

That's everything we're going to cover in the first part of this tutorial. The
second part will dig into the Ember.JS tutorial, as well as setting up our REST
API with `express`.
