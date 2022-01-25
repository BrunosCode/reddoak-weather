<template>
  <div id="app">
    <h1>App Meteo</h1>
    <CityInput @city="searchWeather" />
    <WeatherComponent v-if="displayWeather"
    :city="city" :weather="weather"/>
  </div>
</template>

<script>
import axios from "axios";

import CityInput from './components/CityInput.vue'
import WeatherComponent from './components/WeatherComponent.vue'

export default {
  name: 'App',
  components: {
    CityInput,
    WeatherComponent
  },
  data() {
    return {
      city: "",
      weather: {},
      displayWeather: false
    }
  },
  methods: {
    getWeather() {
      axios.get('https://api.openweathermap.org/data/2.5/weather', {
        params: {
          q: this.city,
          lang: "it",
          appid: "567a30ac0bf63a04687e6450b6c7f1a9"
        }
      })
      .then((res) => {
        this.weather = res.data.weather[0];
        console.log(res.data.weather[0], this.city);
      })
      .catch((e) => {
        console.log(e);
      });
    },
    searchWeather(city) {
      this.city = city[0].toUpperCase() + city.slice(1);
      this.displayWeather = true;
      this.getWeather();
    }
  }
}
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
  color: #2c3e50;

}
</style>
