<template>
    <!-- add background image that dynamically changes with the background -->
    <div class="weatherbox" v-bind:style="{ backgroundImage: 'url(' + require('@/assets/' + theWeather.weather[0].icon + '.jpg') +')' }">
        <div class="inner">
            <h1>Current Weather for {{theWeather.name}}</h1>
            <div>
                <img class="pulse" v-bind:src="'http://openweathermap.org/img/wn/'+ theWeather.weather[0].icon + '@2x.png'" />
                <em>{{theWeather.weather[0].description}}</em>
            </div>
            <div>
                <strong>Current Temperature: </strong>{{theWeather.main.temp}}&deg;<br>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "WeatherBox",
    props: ["theWeather"]
}
</script>


<style scoped>

.weatherbox .inner {
    background: rgba(255,255,255,.75);
    width: 80%;
    margin: 0 auto;
    padding:1em;
    margin-top:3em;
    border-radius: 50px
}
.weatherbox {
    background-size: cover;
    height: 100%;
    width: 100%;
    overflow: auto; 
}
.pulse {
    
    animation: pulse 3s linear infinite;
}
@-webkit-keyframes pulse {
    0% {
        transform: scale(1.2);
    }
    50% {
        transform: scale(.85);
    }
    100% {
        transform: scale(1.2);
    }
}
</style>