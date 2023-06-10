<template>
  <h2>DNI</h2>
  <div class="daily__container" v-for="day in daily" v-bind:key="day.date">
    <p>{{ day.date }}</p>
    <p>{{ day.maxtemp_c }}</p>
    <p>{{ day.mintemp_c }}</p>
    <p>{{ day.avgtemp_c }}</p>
    <p>{{ day.maxwind_hph }}</p>
    <p>{{ day.totalprecip_mm }}</p>
    <p>{{ day.avghumidity }}</p>
    <img src="../assets/64x64/day/113.png" alt="" />
    <!--    <p>{{ day.condition }}</p>-->
  </div>
</template>

<script>
export default {
  name: "DailyItem",
  props: {
    daily: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped></style>
