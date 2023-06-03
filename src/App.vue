<template>
  <div id="app">
    <div class="cell cell-map">
      <MapContainer></MapContainer>
    </div>

    <div v-bind:id="1">
      <h2>{{ weather.location.name }}</h2>
      <p>{{ weather.location.country }}</p>
      <p>{{ weather.location.latitude }}</p>
      <p>{{ weather.location.longitude }}</p>
      <p  >{{ weather.location.timezone }}</p>
    </div>
    <div v-bind:id="2">
      <p>{{ weather.current.temp_c }}</p>
      <p>{{ weather.current.wind_kph }}</p>
      <p>{{ weather.current.wind_dir }}</p>
      <p>{{ weather.current.preasure_mb }}</p>
      <p>{{ weather.current.precip_mm }}</p>
      <p>{{ weather.current.humidity }}</p>
      <p>{{ weather.current.condition }}</p>
    </div>
    <div v-for="day in weather.daily" v-bind:key="day.date">
      <p>{{ day.date }}</p>
      <p>{{ day.maxtemp_c }}</p>
      <p>{{ day.mintemp_c }}</p>
      <p>{{ day.avgtemp_c }}</p>
      <p>{{ day.maxwind_kph }}</p>
      <p>{{ day.totalprecip_mm }}</p>
      <p>{{ day.avghumidity }}</p>
      <p>{{ day.avghumidity }}</p>
      <p>{{ day.condition }}</p>
    </div>
  </div>
</template>

<script>
import MapContainer from './components/MapContainer.vue'

export default {
  name: 'App',
  components: {
    MapContainer
  },
  data() {
    return {
      weather: {
        location: {},
        current: {},
        daily: []
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
  html, body {
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
    grid-row-start: 1;
    grid-row-end: 3;
  }
h2 {
  margin: 40px 0 0;
}
div {
  display: inline-block;
  margin: 0 10px;
}
</style>