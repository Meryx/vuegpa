<template>
  <div id="app">
    <header>
      <h1 id="title">VUE PRACTICE</h1>
    </header>
    <div class="subheader">
      <ul id="navbar">
        <li><a href="">Home</a></li>
        <li><a href="">GPA Calculator</a></li>
      </ul>
    </div>
    <div class="container">
      <GPACalculator />
    </div>
    <footer>
      <p id="footertext">Handcrafted by Anwar to practice Vue.js</p>
    </footer>
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
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100%;
}

footer {
  background-color:#2e2f33;
  margin: 0;
  padding-top: 1.5rem;
  padding-bottom: 1.5rem;
  width: 100%;
  flex-shrink: 0;
  align-self: flex-start;
}

header {
  background-color: #057CCA;
  padding-top: 1.5rem;
  padding-bottom: 1.5rem;
  color: white;

}

.subheader {
  background-color: #0D8DE0;
  margin-bottom: 1.5rem;
  padding-top: 0.1rem;
  padding-bottom: 0.1rem;
  color: white;
  font-weight: bold;
}

.primary {
  color: #00E577;
}

.secondary {
  color: #0D8DE0;
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

#title {
  text-align: left;
  padding: 0;
  padding-left: 0.8rem;
  margin: 0;
  width: 24rem;
  margin: auto;
}

#navbar {
  width: 24rem;
  margin: auto;
  list-style-type: none;
  overflow: hidden;
  padding: 0;

}

#navbar li {
  float: left;
}

#footertext {
  text-align: center;
  color: white;
  font-weight: bold;
}

li a {
  display: block;
  color: white;
  text-decoration: none;
  padding: 0.8rem 1rem;
}

li a:hover {
  color: #00E577;
  text-decoration: underline;
}

#app {
  overflow-x: hidden;
  height: 100%;
  display: flex;
  flex-direction: column;
}


.container {
  flex: 1
}


</style>
