<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <Location />
  </div>
</template>

<script>
import Location from "@/components/Location.vue";

export default {
  name: "Home",
  components: {
    Location
  }
};
</script>
