<template>
  <div id="app" class="App">
    <h1>App Meteo</h1>
    <CityInput @city="searchWeather" />

    <WeatherComponent
      v-if="weatherData.current"
      :city="city"
      :weather="[weatherData.current]"
      >Meteo Oggi</WeatherComponent
    >

    <WeatherComponent
      v-if="weatherData.daily"
      :city="city"
      :multiLine="true"
      :weather="weatherData.daily"
      >Meteo Ogni Giorno</WeatherComponent
    >

    <WeatherComponent
      v-if="weatherData.hourly"
      :city="city"
      :multiLine="true"
      :weather="weatherData.hourly"
      >Meteo Ogni Ora</WeatherComponent
    >
  </div>
</template>

<script>
import axios from "axios";

import CityInput from "./components/CityInput.vue";
import WeatherComponent from "./components/WeatherComponent.vue";

export default {
  name: "App",
  components: {
    CityInput,
    WeatherComponent,
  },
  data() {
    return {
      city: "",
      coord: {},
      weatherData: {},
    };
  },
  methods: {
    // CALL Open Weather Map
    // searchWeather(city) {
    //   this.weather = {};
    //   this.city = city[0].toUpperCase() + city.slice(1);
    //   //this.displayWeather = true;
    //   this.getCoord();
    // },
    // getCoord() {
    //   axios
    //     .get("https://api.openweathermap.org/data/2.5/weather", {
    //       params: {
    //         q: this.city,
    //         lang: "it",
    //         appid: process.env.VUE_APP_MY_OPEN_WEATHER_KEY,
    //       },
    //     })
    //     .then((res) => {
    //       this.coord = res.data.coord;
    //       this.getWeather();
    //     })
    //     .catch((e) => {
    //       console.log(e);
    //     });
    // },
    // getWeather() {
    //   axios
    //     .get("https://api.openweathermap.org/data/2.5/onecall", {
    //       params: {
    //         lat: this.coord.lat,
    //         lon: this.coord.lon,
    //         lang: "it",
    //         appid: process.env.VUE_APP_MY_OPEN_WEATHER_KEY,
    //       },
    //     })
    //     .then((res) => {
    //       this.weather = res.data;
    //       console.log(res.data.current.weather[0], res.data.hourly[0].weather[0].description[0]);
    //     })
    //     .catch((e) => {
    //       console.log(e);
    //     });
    // },

    searchWeather(city) {
      this.weatherData = {};
      this.city = city[0].toUpperCase() + city.slice(1);
      // CALL MY SERVER
      axios
        .get(`${process.env.VUE_APP_MY_SERVER_PORT}/api/weather/${this.city}`)
        .then((res) => {
          this.weatherData = res.data;
          //console.log(res);
        })
        .catch((e) => {
          console.log(e);
        });
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
  background: none;
  border: none;
  &:hover {
    cursor: pointer;
    transform: scale(0.9);
  }

  & .arrow {
    position: relative;
    border: solid white;
    display: inline-block;
    padding: 0.4rem;
    margin-left: 0.5rem;

    &.up {
      border-width: 0 0.2rem 0.2rem 0;
      transform: translateY(-30%) rotate(45deg);
    }

    &.down {
      border-width: 0.2rem 0 0 0.2rem;
      transform: translateY(30%) rotate(45deg);
    }
  }
}

.input {
  border: black 1px solid;
}
</style>
