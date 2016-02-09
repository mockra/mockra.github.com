---
layout: post
title: EmberJS Emoji Component
---
I was looking to add custom emoji to a project I was working on recently, and
wasn't happy with a lot of the options out there. In large part, because a lot
of the libraries were outdated. Here's a simple component I came up with as a
solution.

My first step was creating an emoji service that could handle the actual work.
This allows me to include similar functionality in other components, and keeps
the emojify component from getting too complicated.

I'm not sure if I like the pod structure for services, but I went with it here.
Here's the `app/emoji/service.js` file:

~~~
  import Ember from 'ember';
  const { get } = Ember;

  export default Ember.Service.extend({
    emojiLookup: {
      ':smile:': 'smile'
    },

    emojify(html) {
      var possibleEmojis = html.match(/:([^\s:]+):/g),
          matches = possibleEmojis && possibleEmojis.length || 0,
          foundEmoji;

      for (var i = 0; i < matches; i++) {
        foundEmoji = get(this, 'emojiLookup')[possibleEmojis[i]];
        if (foundEmoji) { html = html.replace(":%@:".fmt(foundEmoji),
          '<img class="emoji" src="/assets/emoji/%@.png">'.fmt(foundEmoji)); }
      }

      return html;
    }
  });
~~~

I then utilize the service in my component.

~~~
  import Ember from 'ember';
  const { computed, get } = Ember;

  export default Ember.Component.extend({
    emoji: Ember.inject.service(),

    formattedContent: computed('content', function() {
      const content = Ember.Handlebars.Utils
        .escapeExpression(get(this, 'content'));
      return get(this, 'emoji').emojify(content);
    })
  });
~~~

In the template we want to tell handlebars not to escape the html:

~~~
{% raw %}
  {{{formattedContent}}}
{% endraw %}
~~~

Depending on how you want to handle your emoji images, you may need to exclude
them from fingerprinting. Here's an example using `ember-cli-build.js`.

~~~
  var EmberApp = require('ember-cli/lib/broccoli/ember-app');

  module.exports = function(defaults) {
    var app = new EmberApp(defaults, {
      fingerprint: {
        exclude: ['assets/emoji']
      }
    });

    return app.toTree();
  };
~~~
