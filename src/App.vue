<template>
  <div id="app">
    <GPACalculator />
  </div>
</template>

<script>
import GPACalculator from './components/GPACalculator.vue'

export default {
  
  name: 'App',
  components: {
    GPACalculator
  },
  
}
</script>

<style>
html, body {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  overflow: hidden;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  overflow-y: scroll;
  height: 100%;
}

h1 {
  text-align: center;
}
</style>
