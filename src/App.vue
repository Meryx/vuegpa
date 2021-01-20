<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
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
  text-align: center;
  color: #2c3e50;
}
#app {

  margin-top: 60px;
}
</style>
