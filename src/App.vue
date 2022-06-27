<template>
  <div id="app">

    <TheHeader />

    <DisksList />

  </div>
</template>

<!-- --------------------------------------------------------------------------- -->

<script>

import TheHeader from "./components/TheHeader.vue";
import DisksList from "./components/DisksList.vue";

export default {
  name: 'App',

  components: {
    TheHeader,
    DisksList,
  },

}
</script>

<!-- --------------------------------------------------------------------------- -->

<style lang="scss">

// Importo il file main di scss
@import "./assets/scss/main.scss";

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
