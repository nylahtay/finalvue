<template>
  <div id="app">
    <!-- THis is where we can set the header text -->
    <Header theTitle="Get the Forcast"/>

    <Input @update="handleUpdate" />
    
    <Weatherbox v-bind:theWeather="weather" />
  </div>
</template>

<script>
//importing the component for the header
import Header from './components/Header.vue'

//importing the component for Input
import Input from './components/Input.vue'

//Import weatherbox
import Weatherbox from './components/Weatherbox.vue'

//importing Bootstrap
import 'bootstrap'
import 'bootstrap/dist/css/bootstrap.min.css'

export default {
  name: 'App',
  components: {
    Header,
    Input,
    Weatherbox
  },
  data()
  {
    //create the weather object
    return {
      weather: [""]
    }
  },
  methods: {
    handleUpdate(info) {
      this.weather = info;
    }
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
}
</style>
