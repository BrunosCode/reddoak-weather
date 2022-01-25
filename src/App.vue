<template>
  <div id="app">
    <h1>App Meteo</h1>
    <CityInput @city="searchWeather" />

    <WeatherSingleLine
      v-if="weather.current"
      :city="city"
      :weather="weather.current.weather[0]"
      >Meteo Oggi</WeatherSingleLine
    >

    <WeatherMultiLine
      v-if="weather.daily"
      :multiLine="true"
      :city="city"
      :weather="weather.daily"
      >Meteo Ogni Giorno</WeatherMultiLine
    >

    <WeatherMultiLine
      v-if="weather.hourly"
      :multiLine="true"
      :city="city"
      :weather="weather.hourly"
      >Meteo Ogni Ora</WeatherMultiLine
    >
  </div>
</template>

<script>
import axios from "axios";

import CityInput from "./components/CityInput.vue";
import WeatherSingleLine from "./components/WeatherSingleLine.vue";
import WeatherMultiLine from "./components/WeatherMultiLine.vue";

export default {
  name: "App",
  components: {
    CityInput,
    WeatherSingleLine,
    WeatherMultiLine,
  },
  data() {
    return {
      city: "",
      coord: {},
      weather: {},
    };
  },
  methods: {
    getCoord() {
      axios
        .get("https://api.openweathermap.org/data/2.5/weather", {
          params: {
            q: this.city,
            lang: "it",
            appid: process.env.VUE_APP_MY_OPEN_WEATHER_KEY,
          },
        })
        .then((res) => {
          this.coord = res.data.coord;
          this.getWeather();
        })
        .catch((e) => {
          console.log(e);
        });
    },
    getWeather() {
      axios
        .get("https://api.openweathermap.org/data/2.5/onecall", {
          params: {
            lat: this.coord.lat,
            lon: this.coord.lon,
            lang: "it",
            appid: process.env.VUE_APP_MY_OPEN_WEATHER_KEY,
          },
        })
        .then((res) => {
          this.weather = res.data;
          console.log(res.data.current.weather[0], res.data.hourly[0].weather[0].description[0]);
        })
        .catch((e) => {
          console.log(e);
        });
    },
    searchWeather(city) {
      this.city = city[0].toUpperCase() + city.slice(1);
      //this.displayWeather = true;
      this.getCoord();
    },
  },
};
</script>

<style lang="scss">
// Reset
*,
*::before,
*::after {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  max-width: 90%;
  margin: 2rem auto;
  color: #2c3e50;
}

.btn {
  color: blue;
  background: none;
  border: none;
  font-weight: 700;
  &:hover {
    cursor: pointer;
    color: darkblue;
    transform: scale(0.9);
  }
}
</style>
