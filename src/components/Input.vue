<template>
    <form>
        <div class="input-group mb-3">
            <div class="input-group-prepend">
                <span class="input-group-text" id="basic-addon1">Zip Code</span>
            </div>
            <input type="text" class="form-control" placeholder="65804" aria-label="Username" aria-describedby="basic-addon1">
        </div>
        <div class="custom-control custom-switch">
            <label class="custom-control-label-before">Celsius</label>
            <input type="checkbox" class="custom-control-input" id="customSwitch1">
            <label class="custom-control-label" for="customSwitch1">Fahrenheit</label>
        </div>
    </form>
</template>


<script>

//importing Axios
import axios from 'axios'

export default {
    name: "Input",
    props:['theWeather'],
    methods : {
        ///Summary: gets the weather using axios get method
        ///Param (zip) : the zip code, default is 65804 for Springfield, MO
        ///Param (units) : the unit of mesurments (metric | imperial), default is metric for celcius
        getWeather(zip = 65804,units = 'metric')
        {
            axios.get('http://api.openweathermap.org/data/2.5/weather?zip='+ zip + ',us&units='+ units +'&appid=884d6cdb392caa239f71a909118eee45')
            .then ( (response) => {
            var weather = response.data;
            this.$emit('update', weather);
            })
        }
    },
    //get weather on load with the default parameters.
    mounted() {
        this.getWeather();
    }
}

</script>

<style scoped>
    label.custom-control-label-before {
        margin-right: 3em;
    }
</style>


