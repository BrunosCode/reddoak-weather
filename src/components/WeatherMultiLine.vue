<template>
  <div class="WeatherMultiLine">

    <div class="WeatherMultiLine__head">
      <h2 class="WeatherMultiLine__title"><slot></slot></h2>
      <button class="btn WeatherMultiLine__btn" @click="showInfo = !showInfo">more info</button>
    </div>

    <div v-if="showInfo">
      <div v-for="(weatherInstant, i) in weather" :key="i" class="WeatherMultiLine__content">
        <h3 class="WeatherMultiLine__time">{{ getDayTime(weatherInstant.dt) }} </h3>
        <h3 class="WeatherMultiLine__weather">{{ weatherInstant.weather[0].description[0].toUpperCase() + weatherInstant.weather[0].description.slice(1) }}</h3>
        <img class="WeatherMultiLine__icon" :src="`http://openweathermap.org/img/w/${ weatherInstant.weather[0].icon }.png`" :alt="weatherInstant.weather[0].description">
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'WeatherMultiLine',
  props: {
    city: {
      type: String,
      required: true
    },
    weather: {
      type: [Object, Array],
      required: true
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
.WeatherMultiLine {
  &__head {
    display: flex;
    justify-content: space-between;
  }



  &__content {
    display: flex;
    justify-content: space-between;
  }
}
</style>
