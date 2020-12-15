<template>
    <form v-on:submit.prevent="onSubmit">
        <div class="input-group mb-3">
            <div class="input-group-prepend">
                <span class="input-group-text" id="basic-addon1">Zip Code</span>
            </div>
            <input type="text" v-model="zip" class="form-control" placeholder="65804" aria-label="Username" aria-describedby="basic-addon1" @keyup="isValid()">
            <div class="input-group-prepend">
                <button type="submit" class="btn btn-primary"> Submit </button>
            </div>
            <div class="invalid-feedback">
                {{feedback}}
            </div>
        </div>
        <div class="custom-control custom-switch">
            <label class="custom-control-label-before">Celsius</label>
            <input type="checkbox" v-model="checked" class="custom-control-input" id="customSwitch1" @change="changeUnit()">
            <label class="custom-control-label" for="customSwitch1">Fahrenheit</label>
        </div>
    </form>
</template>


<script>

//importing Axios
import axios from 'axios'

export default {
    name: "Input",
    data() {
        return{
            //Set the default zip, this updates as the use types in the input
            zip: 65804,
            //set the default units, this updates when the changeUnits() is called
            units : 'metric',
            
            //This is used to determine if the checkbox is checked or not for the units, it auto updates on change
            checked : '',

            feedback : "This is bad"
        }
    },
    methods : {
        ///Summary: gets the weather using axios get method
        ///Param (zip) : the zip code, default is 65804 for Springfield, MO
        ///Param (units) : the unit of mesurments (metric | imperial), default is metric for celcius
        getWeather(zip = this.zip,units = this.units)
        {
            axios.get('https://api.openweathermap.org/data/2.5/weather?zip='+ zip + ',us&units='+ units +'&appid=884d6cdb392caa239f71a909118eee45')
            .then ( (response) => {
            var weather = response.data;
            this.$emit('update', weather);
            })
            .catch(error => {
                console.log(error)
                this.errored = true;
                if (error.response.status == 404) { // tHAT DOES NOT WORK
                    this.feedback = "Error retreaving the Weather: This zip code is not found";
                    document.querySelector('.weatherbox').style.display = 'none';
                    document.querySelector('.invalid-feedback').style.display = 'block';
                }
            })
        },
        ///Summary: when the checkbox changes values this will set the units accordingly.
        ///this also calls the getWeather to get the updated weather in the correct units of measurement.
        changeUnit(){
            if(this.checked){
                this.units = 'imperial';
            }
            else{
                this.units = 'metric';
            }

            //Call the getWeather() to update the weather everytime the switch is changed
            this.getWeather(this.zip, this.units);
        },
        ///Summary: Checks if the zip code is valid
        isValid(){
            //set valid = true
            var valid = true;

            //reset feedback to not display
            document.querySelector('.invalid-feedback').style.display = 'none';

            //regex for a good zip code
            var zipCodePattern = /^\d{5}$|^\d{5}-\d{4}$/;

            //regex to check if there are text characters
            var hasCharacters = /[A-z]/;
            
            //see if zip has text characters
            if(hasCharacters.test(this.zip)){
                valid = false;
                this.feedback = "Zip code cannot contain any letters";
                document.querySelector('.invalid-feedback').style.display = 'block';
            }
            //see if less than 5 characters
            else if(this.zip.length < 5)
            {
                valid = false;
                this.feedback = "Zip code must be at least 5 digits";
                document.querySelector('.invalid-feedback').style.display = 'block';
            }
            //Check if it follows a normal zip format
            else if(!zipCodePattern.test(this.zip)){
                valid = false;
                this.feedback = "Not in a valid zip code format";
                document.querySelector('.invalid-feedback').style.display = 'block';
            }
            return valid;
        },
        ///Summary: this calls the getWeather() whenever the submit button is clicked or the 'enter' key is pressed while in the zip input
        onSubmit(){
            document.querySelector('.weatherbox').style.display = 'block';
            document.querySelector('.invalid-feedback').style.display = 'none';
            //Validate the zip
            if (this.isValid())
            {
                //Call the getWeather() to update the weather everytime the switch is changed
                this.getWeather(this.zip, this.units);
            }
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
    .custom-control-label:before {
        pointer-events: none;
        background-color: #aa00ff;
    }
    .custom-switch .custom-control-label:after {
        background-color: #ffffff;
    }
</style>


