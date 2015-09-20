---
layout: post
title: EmberJS - Get Model Name
---
I recently ran into a problem, where I wanted to share a component between two
different models, but I needed to be aware of which I was using when updating
that record. Here's how you can grab the name of a model if you're using Ember
Data.

Here's an example for a post model:

```
  get(this, 'yourModel.constructor.modelName') === 'post'
```
