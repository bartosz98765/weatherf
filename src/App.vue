<template>
  <div>
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
<!--      <p>{{ day.condition }}</p>-->
    </div>
  </div>
</template>

<script>
export default {
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
        let response = await fetch("http://localhost:8000/main/bialystok");
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

<style scoped>
h2 {
  margin: 40px 0 0;
}
div {
  display: inline-block;
  margin: 0 10px;
}
  </style>