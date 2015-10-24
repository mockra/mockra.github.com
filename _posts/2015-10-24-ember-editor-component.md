---
layout: post
title: Ember Editor Component
---
If you're looking to add your favorite WYSIWYG editor to your Ember
application, it can be difficult knowing where to start. Here's a quick
breakdown on setting up the basics. There will be some differences between
editors, but this approach has worked well for me.

Here's what your component file should look like:

```
  import Ember from 'ember';
  const { set, get } = Ember;

  export default Ember.Component.extend({
    _editor: null,

    didInsertElement() {
      let textarea = this.element.querySelector('#editor');
      // Must be changed.
      let editor = new YourEditor({ element: textarea });
      // Must be changed.
      editor.on('change', () => {
        // Must be changed.
        set(this, 'value', editor.value());
      });
      set(this, '_editor', editor);
    },

    willDestroyElement() {
      // Must be changed.
      get(this, '_editor').destroy();
      set(this, '_editor', null);
    }
  });
```

You'll need to make some changes depending on the API your editor provides. The
first change you'll need to make is to `new YourEditor({})`. This value will
need to be changed to whatever method is used to instantiate your editor.

The second change will be for the change event. Most editors provide a method
for watching for changes to the editor value. You'll want to replace
`.on('change')` with that method.

You'll also need to replace `editor.value()` with the method used to get the
current HTML/Markdown value for your editor. It might be something like
`editor.getHTML()`.

The final change you'll need to make is to the `get(this,
'_editor').destroy();` call. This will need to be updated to whatever method is
used to destroy your editor instance.

Your component template will look like:

```
{% raw %}
  {{textarea value=value id="editor"}}
{% endraw %}
```

Finally, when you want to add an editor for a specific text input, you can use
the following code:

```
{% raw %}
  {{your-editor-component value=post.content}}
{% endraw %}
```
