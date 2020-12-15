<template>
  <div id="app">
    <!-- THis is where we can set the header text -->
    <Header theTitle="Get the Forcast"/>

    <!-- This @update will return the weather object from the Input component weather into the App weather object -->
    <Input @update="handleUpdate" />
    
    <!-- Send the weather object to the weatherbox component -->
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
html, body, #app {
  height: 100%;
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
