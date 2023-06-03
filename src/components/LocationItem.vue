<template>
  <div class="location__container">
    <h2>{{ location.name }}</h2>
    <p>{{ location.country }}</p>
    <p>{{ location.latitude }}</p>
    <p>{{ location.longitude }}</p>
    <p>{{ location.timezone }}</p>
  </div>
</template>

<script>
export default {
  name: "LocationItem",
  props: {
    location: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped></style>
