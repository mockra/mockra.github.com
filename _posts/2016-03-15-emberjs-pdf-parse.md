---
layout: post
title: EmberJS Parse Pdf on Upload
---
If you're building an application that deals with PDF files, then it can be
useful to extract information from a PDF that a user wants to upload. Here's an
example of grabbing the page count from a PDF using the
[pdf.js](https://github.com/mozilla/pdf.js/) library.

The first step is installing the library using bower.

~~~
  bower install pdfjs-dist --save
~~~

Once that's done, we'll need to include the file. This can be done by adding
the following to `ember-cli-build.js`:

~~~
  app.import('bower_components/pdfjs-dist/build/pdf.combined.js');
~~~

Now that we've finished installing the library we're going to use to work with
PDF files, we can write the code for our component. The first thing we'll need
to do is create a `FileReader` in the `init` call of our component.

~~~
  init() {
    this._super(...arguments);
    const fileReader = new FileReader();
    fileReader.onload = get(this, 'parseFile').bind(this);
    this.fileReader = fileReader;
  }
~~~

We'll also need to define the `parseFile` function on our component, which will
handle extracting the page count for us. Here's what that function should look
like:

~~~
  parseFile: async function() {
    const data = new Uint8Array(get(this, 'fileReader').result);
    const pdfData = await PDFJS.getDocument(data);
    set(this, 'pageCount', pdfData.numPages);
  }
~~~

Once our `FileReader` is setup, we can pass it the file in our upload action.
This example assumes that a `fileLoaded` action will be called with the file
the user has selected.

~~~
  actions: {
    fileLoaded: function(file) {
      get(this, 'fileReader').readAsArrayBuffer(file);
    }
  }
~~~

With these three pieces in place, we can show a page count to the user when
they upload their document. If we're looking for a document of a specific size,
we can display a warning message to the user, etc.. `PDFJS` can also be used to
show a preview of the document, as well as a variety of other features.

I've been using the
[ember-cli-file-picker](https://github.com/funkensturm/ember-cli-file-picker)
library for my applications to handle the file selection.
