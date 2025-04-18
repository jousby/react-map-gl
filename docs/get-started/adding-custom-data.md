# Adding Custom Data

## Native Mapbox Layers

You can inject data and mapbox native layers using the [Source](../api-reference/mapbox/source.md) and [Layer](../api-reference/mapbox/layer.md) components:

```tsx
import * as React from 'react';
import Map, {Source, Layer} from 'react-map-gl/maplibre';
import type {CircleLayer} from 'react-map-gl/maplibre';
import type {FeatureCollection} from 'geojson';

const geojson: FeatureCollection = {
  type: 'FeatureCollection',
  features: [
    {
      type: 'Feature',
      geometry: {
        type: 'Point',
        coordinates: [-122.4, 37.8]
      },
      properties: {title: '915 Front Street, San Francisco, California'}
    }
  ]
};

const layerStyle: CircleLayer = {
  id: 'point',
  type: 'circle',
  paint: {
    'circle-radius': 10,
    'circle-color': '#007cbf'
  }
};

function App() {
  return (
    <Map
      initialViewState={{
        longitude: -122.45,
        latitude: 37.78,
        zoom: 14
      }}>
      <Source id="my-data" type="geojson" data={geojson}>
        <Layer {...layerStyle} />
      </Source>
    </Map>
  );
}
```

For details about data sources and layer configuration, check out the [Mapbox style specification](https://www.mapbox.com/mapbox-gl-js/style-spec).

For dynamically updating data sources and layers, check out the [GeoJSON](https://visgl.github.io/react-map-gl/examples/maplibre/geojson) and [GeoJSON animation](http://visgl.github.io/react-map-gl/examples/maplibre/geojson-animation) examples.


## Custom Overlays

You can implement a custom HTML or SVG overlay on top of the map that redraws whenever the camera changes. By calling `map.project()` you can adjust the DOM or CSS properties so that the customly-drawn features are always aligned with the map. See a full example [here](https://github.com/visgl/react-map-gl/tree/8.0-release/examples/maplibre/custom-overlay).


## Other vis.gl Libraries

For more feature rich and performant data visualization overlay use cases, you may consider using other visualization libraries. react-map-gl is part of the [vis.gl](https://www.github.com/visgl) ecosystem, a suite of high-performance data visualization tools for the Web.

- [deck.gl](https://deck.gl) - WebGL-powered framework for the visualization of large datasets.
- [loaders.gl](https://loaders.gl) - loaders for file formats focused on visualization of big data, including point clouds, 3D geometries, images, geospatial formats as well as tabular data.
- [nebula.gl](https://nebula.gl) - 3D-enabled GeoJSON editing based on deck.gl and React.
