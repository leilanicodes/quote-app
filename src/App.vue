<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
    <RandomQuote />
  </div>
</template>

<script>
import RandomQuote from './components/RandomQuote.vue';

export default {
  name: 'App',
  components: {
    RandomQuote,
  },
};
</script>

<style lang="scss">
#app {
  height: 100vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
