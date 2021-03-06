[![Build Status](https://travis-ci.org/mapbox/geo-viewport.svg)](https://travis-ci.org/mapbox/geo-viewport)

# geo-viewport

Turns bounding boxes / extents into centerpoint & zoom
combos for static maps.

Works in node.js and browsers, via [browserify](http://browserify.org/)
or a script tag.

## Install

    npm install --save geo-viewport

Or use a plugin:

```html
<script src='//api.tiles.mapbox.com/mapbox.js/plugins/geo-viewport/v0.1.1/geo-viewport.js'></script>
```

The script-tag include exports an object called `geoViewport`,
with methods `bounds` and `viewport` documented below.

## Example

[Live example with Mapbox Static Map API](https://www.mapbox.com/mapbox.js/example/v1.0.0/static-map-from-bounds-with-geo-viewport/)

### With Node

```js
var geoViewport = require('geo-viewport');

geoViewport.viewport([
    5.668343999999995,
    45.111511000000014,
    5.852471999999996,
    45.26800200000002
], [640, 480])

// yields
// {
//     center: [
//         5.7604079999999955,
//         45.189756500000016
//     ],
//     zoom: 11
// }
```

In a browser:

```html
<script src='//api.tiles.mapbox.com/mapbox.js/plugins/geo-viewport/v0.1.1/geo-viewport.js'></script>
<script>
var bounds = geoViewport.viewport([
    5.668343999999995,
    45.111511000000014,
    5.852471999999996,
    45.26800200000002
], [640, 480]);

var center = geoViewport.bounds(
  [-75.03,
  35.25],
  14,
  [600, 400]);

console.log(bounds);
console.log(center);
</script>
```

## api

### `viewport(bounds, dimensions)`

Given a `WSEN` array of bounds and a `[x, y]` array of pixel
dimensions, return a `{ center: [lon, lat], zoom: zoom }` viewport.

Example:

```js
// first argument is the bounds, and the image is 640x480
geoViewport.viewport([
    5.6683, 45.111, 5.8524, 45.268
], [640, 480])
```

### `bounds(center, zoom, dimensions)`

Given a centerpoint as `[lon, lat]` or `{ lon, lat }`, a zoom,
and dimensions as `[x, y]`, return a bounding box.

Example:

```js
geoViewport.bounds([-75.03, 35.25], 14, [600, 400])
```
