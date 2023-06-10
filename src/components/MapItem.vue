<template>
  <div
    @click="getPosition"
    ref="map-root"
    style="width: 100%; height: 100%"
  ></div>
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
import { toRaw } from "vue";

export default {
  name: "MapItem",
  components: {},
  props: {},
  data() {
    return {
      mousePositionControl: null,
      counter: 0,
    };
  },
  mounted() {
    this.mousePositionControl = new MousePosition({
      coordinateFormat: createStringXY(4),
      projection: "EPSG:4326",
      // className: "custom-mouse-position",
      // target: document.getElementById("mouse-position"),
    });
    new Map({
      controls: defaultControls().extend([this.mousePositionControl]),
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
  methods: {
    getPosition() {
      let mousePositionControlRaw = toRaw(this.mousePositionControl);
      this.$emit("getCoordinates", mousePositionControlRaw.renderedHTML_);
    },
  },
};
</script>
