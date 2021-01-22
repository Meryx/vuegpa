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

input {
  border-color: #FFFFFF;
  border-left-color: #FFFFFF;
  border-left-width: 0.5rem;
  border-right-width: 0.5rem;
  border-top-width: 0;
  border-bottom-width: 0;
  padding: 0.063rem;
  height: 2rem;
  border-left-style:solid;
  border-radius: 0.125rem;
  box-shadow: 0 0 1pt 1pt #d3d3d3;
  outline: 1pt solid #d3d3d3;
}

h1 {
  text-align: center;
}
</style>
