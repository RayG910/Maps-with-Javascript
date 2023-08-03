# Maps-with-Javascript
Built a map using AJAX, NODE-GEOCODER, JS, PUG.


This project demonstrates using AJAX to build a single page application that keeps a list of addresses.

When the user adds a new place, we will perform geocoding server-side. We accomplish this by using node-geocoder.

We then add Lat and Long properties to the database table. 

``const geo = require('node-geocoder');`` 

``const geocoder = geo({ provider: 'openstreetmap' });``


Updating the PUT endpoint to perform geocoding, if a result is found, use the first result. Overwrite the user-provided address with the address returned by the geocorder.

Should look similar to this: 

``const id = await req.db.createPlace(req.body.label, address, lat, lng);``

``res.json({ 
    id: id, 
    label: req.body.label, 
    address: address, 
    lat: lat, 
    lng: lng ``
    
``});``

## Rendering the map

We will use https://leafletjs.com/ to render a map to the screen.

You must include leafletjs's css stylesheet in the header of the HTML page: 

https://unpkg.com/leaflet@1.9.3/dist/leaflet.css

You must also add leafletjs's JavaScript file at the bottom of your page but BEFORE your .js file:

https://unpkg.com/leaflet@1.9.3/dist/leaflet.js


## Adding the map

The HTML will change to include a specific element where the map will be rendered. 

There must be an element with the ``id`` of ``map-container``. There should be a single child element with an ``id`` of ``map``. You can put the ``map-container`` inside a bootstrap column. The following CSS is used: 

`` #map-container {``

   `` position:relative; // important.``
   
   `` height:700px; // pick whatever height you think is nice.``
   
   `` margin-bottom:5rem; // change as you wish``
   
``}``

``#map { // This is required as-is.``

  ``  position: absolute; ``
  
   `` top: 0; ``
   
   `` bottom: 0; ``
   
   `` width: 100%;``
   
``}``

## Initializing the map

### Adding markers and popups 
For each place, we will add a marker with a popup. You should do this when you are looping through the existing places, returned by the ``GET /places`` endpoint. 


``place = {``

   `` id: 42,``
   
  ``  label: 'Ramapo College of New Jersey',``
  
  ``  address: '505 Ramapo Valley Road, Mahwah NJ 07430',``
  
   `` lat: 41.08224455,``
   
   `` lng: -74.1738235180645``
   
``}``


``marker = L.marker([place.lat, place.lng]).addTo(map)``

        ``.bindPopup(`<b>${place.label}</b><br/>${place.address}`)``

### Deleting markers

