---
layout: post
title: Google Places Autocomplete
keywords: [google, places, autocomplete]
---
If you're working on an application that utilizes an input field for addresses,
then adding autocomplete functionality is a great way to improve the user
experience. Google provides a great library and API for implementing this
functionality. You can find this documentation here:

https://developers.google.com/places/documentation/autocomplete

To add support for this library, you'll first need to include it. You can do so
by adding the following script tag to your page.

`<script type="text/javascript"
src="https://maps.googleapis.com/maps/api/js?libraries=places"></script>`

You'll then want to add some code to hook this into your input fields. Here's
an example solution that involves `jQuery`.

{% gist mockra/0e582f02f252877e3d71 %}

You can then add autocomplete to any of your input fields by adding a data
attribute.

`<input id="address" name="address" type="text" data-google-places=true />`

You can see an example of this implementation here:

https://github.com/codeforamerica/MuniciPal/pull/109
