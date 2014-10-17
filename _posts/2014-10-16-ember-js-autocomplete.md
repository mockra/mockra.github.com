---
layout: post
title: EmberJS Autocomplete
---
Adding autocomplete or typeahead to an EmberJS application can be somewhat
challenging if you're just getting started. It definitely requires you to
rethink how you would approach the problem coming from a jQuery background.

Here's an approach I've found that's worked for me, but there's definitely room
for improvement. As I work on my solution, I'll include those updates in this
post. I'm a big fan of `ember-cli`, so the examples in this post will use the
ES6 module syntax.

Here's the corresponding template and controller files we need to setup our
autocomplete field.

`app/templates/posts/new.hbs`
{% gist mockra/34341cef1f093a500e6b %}

There are a couple of interesting things going on here. In our template, we're
setting the value of our input field to `searchText`. We're also iterating
through the `searchResults` array, and initializing our `updateResults`
property. We need to call `updateResults`, so that it will bind to the
`searchText` value - this is something that needs to be cleaned up.

`app/controllers/posts/new.js`
{% gist mockra/1ff031800b1437cf99d1 %}

Our controller is doing the heavy lifting here. It starts off by setting up our
`searchText` and `searchResults` values. The magic is happening with
`updateResults` though.

The magic of EmberJS comes in here by allowing us to bind this function to the
value of `searchText`. Whenever the `searchText` value changes, our function
will run, and update the value of `searchResults`. Which will then be displayed
on the page.

The `searchResults` function starts by grabbing the current value of
`searchText`, and returning if that field is empty. If the input field isn't
empty, then we encode that string, so that it's safe to pass as a URL
parameter. We then use `jQuery` to request a JSON array of strings from our
server. We're finally setting those results to `searchResults`.

An example of a Ruby on Rails server implementing this response through
middleware can be found,
[here](https://github.com/mockra/mtghub/blob/master/app/middleware/search_cards.rb).
