<template>
  <div class="WeatherComponent">
    <h2>Meteo a {{city}}: {{ weather.description[0].toUpperCase() + weather.description.slice(1) }}</h2>
    <img :src="`http://openweathermap.org/img/w/${weather.icon}.png`" :alt="weather.description">
  </div>
</template>

<script>
export default {
  name: 'WeatherComponent',
  props: {
    city: {
      type: String,
      required: true
    },
    weather: {
      type: Object,
      required: true
    },
  }
}
</script>

<style scoped lang="scss">

</style>
