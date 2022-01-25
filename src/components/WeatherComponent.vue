<template>
  <div class="WeatherComponent">

    <div class="WeatherComponent__head">
      <h2 class="WeatherComponent__title"><slot></slot> a {{city}}</h2>
      <button class="btn" @click="showInfo = !showInfo">
        <i v-if="showInfo" class="arrow down"></i>
        <i v-else class="arrow up"></i>
      </button>
    </div>

    <transition name="slide">
      <div v-if="showInfo">
        <div v-for="(weatherInstant, i) in weather" :key="i" class="WeatherComponent__content">
          <h4 class="WeatherComponent__time">{{ getDayTime(weatherInstant.dt) }} </h4>
          <h3 class="WeatherComponent__weather">{{ weatherInstant.weather[0].description[0].toUpperCase() + weatherInstant.weather[0].description.slice(1) }}</h3>
          <img class="WeatherComponent__icon" :src="`http://openweathermap.org/img/w/${ weatherInstant.weather[0].icon }.png`" :alt="weatherInstant.weather[0].description">
        </div>
      </div>
    </transition>

  </div>
</template>

<script>
export default {
  name: 'WeatherComponent',
  props: {
    weather: {
      type: [Object, Array],
      required: true
    },
    city: {
      type: String,
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
      let italianDays = [
        "Domenica",
        "Lunedì",
        "Martedì",
        "Mercoledì",
        "Giovedì",
        "Venerdì",
        "Sabato"
      ]
      let formatedDayTime = `${italianDays[dayTime.getDay()]} alle ${dayTime.toLocaleTimeString('it-IT', { hour: '2-digit', minute: '2-digit' })}`;
      return formatedDayTime;
    }
  }
}
</script>

<style scoped lang="scss">
.WeatherComponent {

  border-radius: 2rem;
  margin-bottom: .5rem;
  background-color: rgb(230, 230, 230);

  &__head {
    border-radius: 2rem;
    padding: 1rem 2rem;
    background-color: rgb(0, 0, 0);
    color: white;
    display: flex;
    justify-content: space-between;
  }


  &__content {
    padding: .5rem 1rem;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    justify-items: center;
    align-items: center;
  }
}

.slide {
  &-enter-active, &-leave-active {
     transition: ease-in-out 0.5s;
  }
  
  &-enter-to, &-leave {
     max-height: 100%;
     overflow: hidden;
  }
  
  &-enter, &-leave-to {
     overflow: hidden;
     max-height: 0;
  }
}
</style>
