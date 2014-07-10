dc.leaflet.js
=============
This extension provides support for DC.js charts in a Leaflet.js map.

Demo
=============
Examples can be found here:
[http://opendata.yurukov.net/demo/dcjs_leaflet/](http://opendata.yurukov.net/demo/dcjs_leaflet/)

Requirements
=============
*  [dc.js](https://github.com/dc-js/dc.js) 1.7.0 ([crossfilter.js](https://github.com/square/crossfilter) 1.3.7 & [d3.js](https://github.com/mbostock/d3) 3.4.8)
*  [leaflet.js](https://github.com/Leaflet/Leaflet) 0.7.2
*  [leaflet.markercluster.js](https://github.com/Leaflet/Leaflet.markercluster) 0.4.0 (in case you use the cluster option)

The charts should work with older versions with minor changes.

Usage
=============
There are two charts currently implemented - markers and choropleth. They extend the base abstract leaflet chart. Both support selection of datapoints and update in real time. Styling and map options can be set directly to the map object and though functions in the chart. Check the [Leaflet reference](http://leafletjs.com/reference.html#map-options) for more information on the specific map, marker and geojson options. 
Location can be set as either 'lat,lng' string or as an array [lat,lng].

Marker chart
--------------------
Each group is presented as one marker on the map. 
```
dc.leafletMarkerChart(parent,chartGroup)
  .mapOptions({..})       - set leaflet specific options to the map object; Default: Leaflet default options
  .center([1.1,1.1])      - initial location
  .zoom(7)                - initial zoom level
  .map()                  - get map object
  .locationAccessor()     - function (d) to access the property indicating the latlng (string or array); Default: keyAccessor
  .marker()               - set function (d,map) to build the marker object. Default: standard Leaflet marker is built
  .icon()                 - function (d,map) to build an icon object. Default: L.Icon.Default
  .popup()                - function (d,marker) to return the string or DOM content of a popup
  .renderPopup(true)      - set if popups should be shown; Default: true
  .cluster(false)         - set if markers should be clustered. Requires leaflet.markercluster.js; Default: false
  .clusterObject({..})    - options for the markerCluster object
  .rebuildMarkers(false)  - set if all markers should be rebuild each time the map is redrawn. Degrades performance; Default: false
  .brushOn(true)          - if the map would select datapoints; Default: true
  .filterByArea(false)    - if the map should filter data based on the markers inside the zoomed in area instead of the user clicking on individual markers; Default: false
  .markerGroup()          - get the Leaflet group object containing all shown markers (regular group or cluster)
```

Choropleth chart
--------------------
Each group is mapped to an feature on the map
```
dc.leafletChoroplethChart(parent,chartGroup)
  .mapOptions({..})       - set leaflet specific options to the map object; Default: Leaflet default options
  .center([1.1,1.1])      - get or set initial location
  .zoom(7)                - get or set initial zoom level
  .map()                  - get map object
  .geojson()              - geojson object describing the features
  .featureOptions()       - object or a function (feature) to set the options for each feature
  .featureKeyAccessor()   - function (feature) to return a feature property that would be compared to the group key; Defauft: feature.properties.key
  .popup()                - function (d,feature) to return the string or DOM content of a popup
  .renderPopup(true)      - set if popups should be shown; Default: true
  .brushOn(true)          - if the map would select datapoints; Default: true
```
