<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <VacationPicker />
  <CountryDetail />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
 import VacationPicker from "./components/VacationPicker";
 import CountryDetail from "./components/countryDetail.vue"


export default {
  name: 'App',
  components: {
    HelloWorld,VacationPicker,CountryDetail 
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
