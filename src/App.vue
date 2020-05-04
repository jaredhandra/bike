<template>
  <div id="app">
    <div class="container">
      <div id="nav"></div>
      <router-view />
    </div>
  </div>
</template>

<style lang="scss">
@import "../node_modules/nes.css/css/nes.css";
@import url("https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap");
body {
  font-family: "Press Start 2P", cursive;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
  margin-top: 150px;
}
</style>
