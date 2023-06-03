<template>
  <form @submit="onSubmit" class="daily__location_form">
    <div class="daily__location_form_input">
      <label>Podaj nazwę miejsowości</label>
      <input type="text" v-model="city" name="city" placeholder="miejscowość" />
    </div>
    <input type="submit" value="Wyświetl pogodę" class="btn btn-block" />
  </form>
</template>

<script>
export default {
  name: "LocationForm",

  data() {
    return {
      city: "",
      latitude: "",
      longitude: "",
    };
  },

  methods: {
    onSubmit(e) {
      e.preventDefault();
      if (!this.city) {
        alert("Proszę podać nazwę miejscowości");
        return;
      }
      this.$emit("cityInput", this.city);
      this.city = "";
    },
  },
};
</script>

<style scoped></style>
