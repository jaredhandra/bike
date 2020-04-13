<template>
  <div>
    <button id="location-button" @click="getLocation()">Send location</button>
  </div>
</template>

<script>
import axios from "axios";
import constants from "../../constants";

export default {
  name: "Location",
  data() {
    return {
      currentLocation: null,
      gettingLocation: false,
      error: null
    };
  },
  methods: {
    getLocation() {
      if (!("geolocation" in navigator)) {
        this.error = "Geolocation is not available.";
        return;
      }
      // get position
      navigator.geolocation.getCurrentPosition(
        pos => {
          this.gettingLocation = false;
          this.currentLocation = pos;
          this.getWeatherData();
        },
        err => {
          this.gettingLocation = false;
          this.error = err.message;
        }
      );
    },
    getWeatherData() {
      if (this.currentLocation && !this.gettingLocation) {
        axios
          .get("https://kob50kazlg.execute-api.us-east-1.amazonaws.com/conditions?", {
            params: {
              long: this.currentLocation.coords.longitude,
              lat: this.currentLocation.coords.latitude
            }
          })
          .then(response => {
            console.log(response);
          })
          .catch(response => {
            console.log(response);
          });
      }
    }
  }
};
</script>

<style lang="scss" scoped></style>
