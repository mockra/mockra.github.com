---
layout: post
title: Liquid Fire - EmberJS Transitions
---
Front-End applications are starting to feel more and more like native
applications, and adding transitions to your website is a great way to
enhance that experience. Like most things involving EmberJS, adding
transitions is a breeze.

There are a lot of solutions out there geared towards adding rich animations
to web applications. One of my favorite solutions is [Famous](http://famo.us),
but with EmberJS, I like to use
[liquid-fire](http://ef4.github.io/liquid-fire/#/transitions/primitives).

Liquid Fire makes adding transitions between Ember routes incredibly easy. It
uses [velocity](http://julian.com/research/velocity/) to power its animations,
and provides a nice DSL for adding transitions to your Ember app.

To get started with liquid-fire, you'll first need to add the library to your
Ember CLI application.

`npm install --save-dev liquid-fire`

Once that's done, you can swap your `{{"{{outlet"}}}}` helper with
`{{"{{liquid-outlet"}}}}`. You'll then need to create an `app/transitions.js` file
that will define your transitions.

Here's an example that adds a swipe left/right feel to your transitions.

```
  export default function(){
    this.transition(
      this.fromRoute('people.index'),
      this.toRoute('people.detail'),
      this.use('toLeft'),
      this.reverse('toRight')
    );
  };
```
