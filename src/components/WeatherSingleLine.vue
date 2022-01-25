<template>
  <div class="WeatherComponent">

    <div class="WeatherComponent__head">
      <h2 class="WeatherComponent__title"><slot></slot></h2>
      <button class="btn WeatherComponent__btn" @click="showInfo = !showInfo">more info</button>
    </div>

    <div v-if="showInfo" class="WeatherComponent__content">
      <h3 class="WeatherComponent__time">{{ getDayTime(weather.dt) }} </h3>
      <h3 class="WeatherComponent__weather">{{ weather.description[0].toUpperCase() + weather.description.slice(1) }}</h3>
      <img class="WeatherComponent__icon" :src="`http://openweathermap.org/img/w/${ weather.icon }.png`" :alt="weather.description">
    </div>

    <!-- <div v-else>
      <div v-for="(weatherInstant, i) in weather" :key="i" class="WeatherComponent__content">
        <h3 class="WeatherComponent__time">{{ weatherInstant.dt }}</h3>
        <h3 class="WeatherComponent__weather">{{ weatherInstant.weather[0].description[0].toUpperCase() + weatherInstant.weather[0].description.slice(1) }}</h3>
        <img class="WeatherComponent__icon" :src="`http://openweathermap.org/img/w/${ weatherInstant.weather[0].icon }.png`" :alt="weatherInstant.weather[0].description">
      </div>
    </div> -->

  </div>
</template>

<script>
export default {
  name: 'WeatherSingleLine',
  props: {
    city: {
      type: String,
      required: true
    },
    weather: {
      type: [Object, Array],
      required: true
    },
    multiLine: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      showInfo: false,
    }
  },
  methods: {
    getDayTime(instant) {
      let dayTime = new Date(instant * 1000);
      let formatedDayTime = `${dayTime.toLocaleDateString('it-IT')} ${dayTime.toLocaleTimeString('it-IT')}`;
      return formatedDayTime;
    }
  }
}
</script>

<style scoped lang="scss">
.WeatherComponent {
  &__head {
    display: flex;
    justify-content: space-between;
  }



  &__content {
    display: flex;
    justify-content: center;
  }
}
</style>
