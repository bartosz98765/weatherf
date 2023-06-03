<template>
  <div id="app">
    <div class="cell cell-location-form">
      <LocationForm></LocationForm>
    </div>
    <div class="cell cell-location">
      <LocationItem :location="weather.location"></LocationItem>
    </div>
    <div class="cell cell-map">
      <MapItem></MapItem>
    </div>
    <div class="cell cell-current">
      <CurrentItem :current="weather.current"></CurrentItem>
    </div>
    <div class="cell cell-daily">
      <DailyItem :daily="weather.daily"></DailyItem>
    </div>
  </div>
</template>

<script>
import MapItem from "./components/MapItem.vue";
import LocationForm from "./components/LocationForm.vue";
import LocationItem from "./components/LocationItem.vue";
import CurrentItem from "./components/CurrentItem.vue";
import DailyItem from "./components/DailyItem.vue";

export default {
  name: "App",
  components: { LocationForm, MapItem, LocationItem, CurrentItem, DailyItem },
  data() {
    return {
      weather: {
        type: Object,
        required: true,
      },
    };
  },

  methods: {
    async getData() {
      try {
        let response = await fetch("http://localhost:8000/main/warszawa");
        this.weather = await response.json();
      } catch (error) {
        console.log(error);
      }
    },
  },

  created() {
    this.getData();
  },
};
</script>

<style>
html,
body {
  height: 100%;
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  display: grid;
  grid-template-columns: 100vh;
  grid-auto-rows: 1fr;
  grid-gap: 1rem;
  padding: 1rem;
  box-sizing: border-box;
}

.cell {
  border-radius: 4px;
  background-color: lightgrey;
}

.cell-map {
  grid-column: 1;
  grid-row: 3;
}

.cell-location {
  grid-column: 3;
  grid-row: 3;
}

.cell-current {
  grid-column: 2;
  grid-row: 3;
}

.cell-daily {
  grid-column: 1 / 4;
  grid-row: 2;
}

h2 {
  margin: 40px 0 0;
}

div {
  display: inline-block;
  margin: 0 0;
}
</style>
