<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="WCLOSET"/>
  </div>
</template>

<script>

import HelloWorld from './components/HelloWorld.vue'
export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Gaegu&family=Poor+Story&family=Roboto&display=swap');

#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  /* font-family: 'Gaegu', cursive; */
  /* font-family: 'Roboto', sans-serif; */
  font-family: 'Poor Story', cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
