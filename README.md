# Leaflet Data Table

Work In Progress. Very experimental.

Dead simple data table for leaflet layers.

View index.html or [checkout the example](http://diogok.net/leaflet.table).

## Features

Done:

- Data table overlay
- Keyboard navigation
- Click on line to focus marker
- Click on marker to focus line
- Open/close
- Multiple tables
- Filter

Not done:

- Editor
- Two way sync between data, editor and layer
- Add row
- Add columns
- Remove row
- Remove columns

## Usage

Start with the basic Leaflet HTML:

```html
<!-- Leaflet CSS and JS -->
<link rel="stylesheet" href="http://cdnjs.cloudflare.com/ajax/libs/leaflet/0.7.3/leaflet.css" />
<script src="http://cdnjs.cloudflare.com/ajax/libs/leaflet/0.7.3/leaflet.js"></script>

<!-- table CSS and JS -->
<link rel="stylesheet" href="leaflet.table.css" />
<script src="leaflet.table.js" type="text/javascript"></script>

<!-- basic style -->
<style>
  body {
    margin: 0;
    padding: 0;
  }
  #map {
    width: 100vw;
    height: 100vh;
  }
</style>

<!-- leaflet container -->
<div id="map">
</div>
```

Prepare your data:

```javascript
// start leaflet
var map = L.map('map').setView([0, 0], 1);
L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png').addTo(map);

// some demo markers
var marker1 = new L.marker([50.50,21.21],{ });
marker1.bindPopup('ID: 1');
// populate the data to show on the table
marker1.properties = {
  id: 1,
  foo: "bar",
  fuz: "baz"
};

var marker2 = new L.marker([50.51,22.22],{ });
marker2.bindPopup('ID: 2');
// populate the data to show on the table
marker2.properties = {
  id: 2,
  foo: "bar2",
  fuz: "baz2"
};

var marker3 = new L.marker([50.53,22.23],{ });
marker2.bindPopup('ID: 3');
// populate the data to show on the table
marker2.properties = {
  id: 3,
  foo: "bar3",
  fuz: "baz3"
};

// we create a group to hold the table data
var group = new L.layerGroup([marker1,marker2,marker3]);
// or  group.addLayer(marker1)  and etc
group.addTo(map);

// and finally the table
var table = L.control.table({
  tables:[ // you can have multiple tables
    {
      name: "Group1", 
      layer: group, // layer of first table
      id: "id", // propertie that uniquely identifies each line
      fields: ['id','foo','fuz'] // list of fields to display
    }
  ],
  collapsed: true // to start collapsed
})

table.addTo(map);
```

You can also use FeatureLayer and GeoJson layers just like LayerGroup.


## License

MIT

