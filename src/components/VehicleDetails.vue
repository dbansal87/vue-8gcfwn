<template>
  <div id="rightsideDetails">
    <div v-for="(value, key) in vehiclesItem" :key="key">
      {{ key }} : {{ value }}
    </div>
  </div>
</template>

<script>
export default {
  name: "VehicleDetails",
  props: {
    vehiclesItem: Object,
  },
  mounted() {
    console.log("vehiclesItem", this.vehiclesItem);
  },
};
</script>
<style scoped>
#rightsideDetails {
  background-color: cadetblue;
}
</style>
