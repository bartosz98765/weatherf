<template>
  <div id="app">
    <div class="cell cell-location">
      <LocationItem :location="weather.location"></LocationItem>
    </div>
    <div class="cell cell-map">
      <MapItem></MapItem>
    </div>
    <div class="cell cell-current">
      <CurrentItem :current="weather.current"></CurrentItem>
    </div>
    <div class="cell cell-daily">Daily</div>

    <!--    <div v-for="day in weather.daily" v-bind:key="day.date">-->
    <!--      <p>{{ day.date }}</p>-->
    <!--      <p>{{ day.maxtemp_c }}</p>-->
    <!--      <p>{{ day.mintemp_c }}</p>-->
    <!--      <p>{{ day.avgtemp_c }}</p>-->
    <!--      <p>{{ day.maxwind_kph }}</p>-->
    <!--      <p>{{ day.totalprecip_mm }}</p>-->
    <!--      <p>{{ day.avghumidity }}</p>-->
    <!--      <p>{{ day.avghumidity }}</p>-->
    <!--      <p>{{ day.condition }}</p>-->
    <!--    </div>-->
  </div>
</template>

<script>
import MapItem from "./components/MapItem.vue";
import LocationItem from "./components/LocationItem.vue";
import CurrentItem from "./components/CurrentItem.vue";

export default {
  name: "App",
  components: { MapItem, LocationItem, CurrentItem },
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
  height: 100%;
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
  grid-row: 2;
}

.cell-location {
  grid-column: 3;
  grid-row: 2;
}

.cell-current {
  grid-column: 2;
  grid-row: 2;
}

.cell-daily {
  grid-column: 1 / 4;
  grid-row: 1;
}

h2 {
  margin: 40px 0 0;
}

div {
  display: inline-block;
  margin: 0 0;
}
</style>
