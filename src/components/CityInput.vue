<template>
  <div class="CityInput">
    <input v-model="city" type="text" name="city" id="city">
    <button class="btn" @click="emitWeather" @keypress.enter="emitWeather">Get Weather</button>
  </div>
</template>

<script>
export default {
  name: 'CityInput',
  data() {
    return {
      city: ""
    }
  },
  methods: {
    emitWeather() {
      this.$emit("city", this.city);
    }
  }
}
</script>

<style scoped lang="scss">

</style>
