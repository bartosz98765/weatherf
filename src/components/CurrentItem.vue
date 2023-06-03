<template>
  <div v-if="current" class="current__container">
    <h2>OBECNIE</h2>
    <p>{{ current.temp_c }}</p>
    <p>{{ current.wind_kph }}</p>
    <p>{{ current.wind_dir }}</p>
    <p>{{ current.preasure_mb }}</p>
    <p>{{ current.precip_mm }}</p>
    <p>{{ current.humidity }}</p>
    <p>{{ current.condition }}</p>
  </div>
</template>

<script>
export default {
  name: "CurrentItem",
  props: {
    current: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped></style>
