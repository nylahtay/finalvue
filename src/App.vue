<template>
  <div id="app">
    <!-- THis is wher we can set the header text -->
    <Header theTitle="Get the Forcast"/>
    <Input />
  </div>
</template>

<script>
//importing the component for the header
import Header from './components/Header.vue'

//importing the component for Input
import Input from './components/Input.vue'

//importing Axios
import axios from 'axios'

//importing Bootstrap
import 'bootstrap'
import 'bootstrap/dist/css/bootstrap.min.css'

export default {
  name: 'App',
  components: {
    Header,
    Input
  },
  data()
  {
    //this is the test data that I was working with,
    return {
      weather: [
        
      ]
    }
  },
  //this is the TV show json.
  mounted()
  {
    axios.get('http://api.openweathermap.org/data/2.5/weather?zip=65804,us&appid=884d6cdb392caa239f71a909118eee45')
    .then ( (response) => {
      this.weather = response.data;
    })
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
