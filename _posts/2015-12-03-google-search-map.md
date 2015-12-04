---
layout: post
title: Google Search Map
---
If your application offers a location based search page, then adding an
interactive map can be a great way to help users find new locations. It also
adds a polished feel to your search page. Here's a brief look at how you can
add an interactive map using the google maps API.

The first thing you'll need to do is come up with coordinates for your user's
location. Depending on your search functionality, this can happen on the server
or client side. Once you have your coordinates, you can add them to a map
container. Here's an example using `ruby/erb`.

```
  <div id="map-container" data-lat=<%= @location.latitude %>
    data-lng=<%= @location.longitude %>></div>
```

You'll need to provide some basic styling for your map-container. Here's some
sample CSS to get you started:

```
  #map-container {
    margin-top: 40px
    height: 600px
    width: 80%
    background-color: white
    background-repeat: no-repeat
    background-position: center
    margin-left: auto
    margin-right: auto
    outline: 1px solid gray
    outline-offset: 4px
  }
```

Once you have your markup finished, we can add the javascript necessary
to get your map working. The first thing you'll need to do is include the
google places library, you can do so with the following script tag:

```
  <script type="text/javascript" src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&libraries=places"></script>
```

You'll then need to add some javascript for displaying the map in your
container. Here's the coffeescript for doing that:

```
  $ ->
    if $('#map-container').length > 0
      latitude = parseFloat($('#map-container').data('lat'))
      longitude = parseFloat($('#map-container').data('lng'))

      map = new google.maps.Map(document.getElementById('map-container'), {
        center: { lat: latitude, lng: longitude },
        zoom: 14
      })

      google.maps.event.addListener map, 'bounds_changed', ->
        $.ajax({
          type: 'POST',
          url: '/api/marker-endpoint',
          data: { coords: map.getBounds().toUrlValue() },
          success: googleAddMarkers.bind(map)
        })
```

Most of the logic here is just to turn our map container into an interactive
map using google's library. The main difference you'll notice is at the end.
We've added an event listener for `bounds_changed`.

This event listener will submit a request to an endpoint you've setup on your
server. Your endpoint will take the bounding values provided by our map, and
return an array of locations within that bounding box. This is how we'll show
markers for each location returned by your search.

Here's an example endpoint using Ruby on Rails and the Geocoder library.

```
  render json: Location.within_bounding_box(params[:coords].split(','))
    .pluck(:lat, :lng, :name, :id)
```

We're searching locations using the coordinates provided by our map container,
and then grabbing the latitude, longitude, name, and id of our location. You
only need to return the latitude and longitude, but it's helpful to provide a
title and id for our markers. These values will allow us to provide labels and
URLs for our markers.

Once we've finished adding our endpoint, we can add the `googleAddMarkers`
function to our javascript.

```
  googleAddMarkers = (data) ->
    map = this
    $.each data, (index, location) ->
      marker = new google.maps.Marker({
        position: {lat: Number(location[0]), lng: Number(location[1])},
        map: map,
        title: location[2],
        url: '/locations/' + location[3]
      })
      google.maps.event.addListener marker, 'click', ->
        window.location.href = this.url
```

You'll need to update this function to work with your API response, but the key
attributes you need to provide are the `position` and `map`. The title is used
for adding a label to the marker, and the url is added for our click handler.

If you're not returning a URL to use with your markers, you can remove the
click event listener. It's designed to turn the markers on your map into links
that the user can click on.

While you'll likely need to make some changes to get the map working for you
specific application, this is a great starting point to help you get there.
Good luck!
