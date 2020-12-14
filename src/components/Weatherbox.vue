<template>
    <div class="weatherbox">
        <h1>Current Weather for {{theWeather.name}}</h1>
        <div>
            <img class="pulse" v-bind:src="'http://openweathermap.org/img/wn/'+ theWeather.weather[0].icon + '@2x.png'" />
            <em>{{theWeather.weather[0].description}}</em>
        </div>
        <div>
            <strong>Current Temperature: </strong>{{theWeather.main.temp}}<br>
            <strong>High: </strong>{{theWeather.main.temp_max}}<br>
            <strong>Low: </strong>{{theWeather.main.temp_min}}<br>
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