---
layout: post
title: EmberJS - Google Places
---
Adding auto complete to an address field can be done using the Google Places
library. Like most things involving EmberJS, this can be done using a
component.

You'll first need to include the google places library. You can find that
script
[here](https://maps.googleapis.com/maps/api/js?v=3.exp&libraries=places).

You can include it in a script tag, or add it to the vendor directory, and
import it in your `Brocfile.js`.

Once that's done, you can create your component using the following code:

~~~
  import Ember from 'ember';

  export default Ember.TextField.extend({
    type: 'text',

    didInsertElement: function() {
      var options = {
        types: ['geocode'],
        componentRestrictions: {country: 'us'}
      };
      new google.maps.places.Autocomplete(this.$()[0], options);
    }
  });
~~~

This component builds on `Ember.TextField` to watch for inserts, and then
correspondingly updates the auto complete results.
