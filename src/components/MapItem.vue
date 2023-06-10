<template>
  <div ref="map-root" style="width: 100%; height: 100%"></div>
  <div id="mouse-position"></div>
</template>

<script>
import Map from "ol/Map";
import MousePosition from "ol/control/MousePosition.js";
import OSM from "ol/source/OSM";
import TileLayer from "ol/layer/Tile";
import View from "ol/View";
import { createStringXY } from "ol/coordinate.js";
import { defaults as defaultControls } from "ol/control.js";
import "ol/ol.css";

export default {
  name: "MapItem",
  components: {},
  props: {},
  mounted() {
    const mousePositionControl = new MousePosition({
      coordinateFormat: createStringXY(4),
      projection: "EPSG:4326",
      // className: "custom-mouse-position",
      // target: document.getElementById("mouse-position"),
    });
    new Map({
      controls: defaultControls().extend([mousePositionControl]),
      target: this.$refs["map-root"],
      layers: [
        new TileLayer({
          source: new OSM(),
        }),
      ],

      view: new View({
        zoom: 7,
        center: [2275000, 6808000],
        constrainResolution: true,
      }),
    });
  },
};
</script>
