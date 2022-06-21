<template>
  <div>
    <h1>{{ msg }}</h1>
    <div class="flex-container">
      <div id="leftsideMenu">
        <ul>
          <li v-for="vehicle in vehicles" :key="vehicle.name">
            <a v-on:click="onSelected(vehicle)">{{ vehicle.name }}</a>
          </li>
        </ul>
      </div>
      <div id="rightsideDetails">
        <VehicleDetails :vehiclesItem="selectedVehicle" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import VehicleDetails from "./VehicleDetails";
export default {
  name: "VehicleList",
  components: {
    VehicleDetails,
  },
  data() {
    return {
      vehicles: [],
      selectedVehicle: {},
    };
  },
  props: {
    msg: String,
  },
  mounted() {
    console.warn("inside mount");
    this.fetchVehicles();
  },
  methods: {
    async fetchVehicles() {
      try {
        const url = "api/vehicles/";
        const response = await axios.get(url);
        const results = response.data.results;
        this.vehicles = results;
      } catch (err) {
        console.log("Error:", err);
      }
    },
    onSelected(vehicle) {
      console.log("onSelected");
      this.selectedVehicle = vehicle;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.flex-container {
  display: flex;
  background-color: darkgrey;
}
.flex-container > div {
  border: 1px solid black;
  color: white;
  width: 50%;
  margin: 0px;
  text-align: center;
  line-height: 25px;
  font-size: 15px;
}
ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}
#rightsideDetails {
  background-color: cadetblue;
}
#leftsideMenu ul li {
  border-bottom: 1px dashed lightgray;
  background-color: darkgray;
}
#leftsideMenu ul li a {
  color: white;
  display: block;
  padding: 8px 20px 8px 20px;
}
#leftsideMenu ul li a:hover {
  background-color: black;
  transition: 0.5s;
  padding-left: 30px;
  padding-right: 10px;
}
</style>
