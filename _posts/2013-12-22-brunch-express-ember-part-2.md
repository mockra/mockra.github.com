---
layout: post
title: Brunch, Express, and Ember.JS Guide - Part 2
---
The second part of this guide is going to focus on building out our REST API,
and adding MongoDB to the mix. Relevant links from the previous tutorial are
listed below.

  * [Part 1](http://mockra.com/2013/12/19/brunch-express-ember-part-1/)
  * [Example on Github](https://github.com/mockra/express_ember_example)

### Todo Model
In order to return a list of todos, we'll first need to create a Schema
definition for our todo. We'll set this up in the `server/models/todo.js` file.

{% gist 8141793 %}

Mongoose provides a clean API for working with MongoDB that makes setting up
our models fairly painless.

### Todo Routes
We can now add the various routes for listing, creating, updating, and deleting
todos. We're going to list our routes in `server/routes.js`. This file will be
responsible for requiring our controllers, and mapping specific paths to
controller methods.

{% gist 8141935 %}

We'll also need to require our `server/routes.js` file in `server.js`. This is
done on `line 22`.

{% gist 8141958 %}

### Todos Controller
Our next step will be creating the controller that's going to handle our route
actions. We'll do this by creating the `server/controllers/todos.js` file
specified in our `routes.js` file.

{% gist 8142625 %}

### Tutorial Changes
Our back-end is now prepared to handle the Getting Started Ember.JS tutorial.
We will need to make some small changes to the tutorial for it to function
correctly with Ember Data.

The changes we'll be making are to `app/controllers/todos_controller.js`, and
`app/routes/todos.js`.

In `todos_controller.js`, on line 9, you need to change `'todo'` to `App.Todo`.

{% gist 8142638 %}

In `todos.js`, on lines 15 and 26, you'll also need to update `'todo'` to
`App.Todo`.

{% gist 8142655 %}
