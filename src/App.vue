<template>
  <div id="app">
    <div class="cell cell-location-form">
      <LocationForm @cityInput="onLocationForm"></LocationForm>
    </div>
    <div class="cell cell-location">
      <LocationItem :location="weather.location"></LocationItem>
    </div>
    <div class="cell cell-map">
      <MapItem @getCoordinates="onMapForm"></MapItem>
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
      city: "lodz",
    };
  },

  methods: {
    async getData(city) {
      try {
        let response = await fetch(`http://localhost:8000/main/${city}`);
        this.weather = await response.json();
      } catch (error) {
        console.log(error);
      }
    },
    onLocationForm(value) {
      this.city = value;
      this.getData(this.city);
    },
    onMapForm(value) {
      const coordinates = value.split(",").reverse().toString();
      this.getData(coordinates);
    },
  },

  created() {
    this.getData(this.city);
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
  grid-gap: 3px;
  padding: 4px;
  box-sizing: border-box;
}

.cell {
  border-radius: 4px;
  background-color: lightblue;
}

.cell-location-form {
  grid-column: 1 / 4;
  grid-row: 1;
}

.cell-map {
  grid-column: 1;
  grid-row: 4;
}

.cell-location {
  grid-column: 3;
  grid-row: 4;
}

.cell-current {
  grid-column: 2;
  grid-row: 4;
}

.cell-daily {
  grid-column: 1 / 4;
  grid-row: 3;
}

h2 {
  margin: 40px 0 0;
}

div {
  display: inline-block;
  margin: 0 0;
}
</style>
