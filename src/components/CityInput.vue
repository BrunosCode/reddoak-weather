<template>
  <div class="CityInput">
    <input
      class="input CityInput__input"
      v-model="city"
      type="text"
      name="city"
      id="city"
    />
    <button
      class="btn CityInput__btn"
      @click="emitWeather"
      @keypress.enter="emitWeather"
    >
      Cerca
    </button>
  </div>
</template>

<script>
export default {
  name: "CityInput",
  data() {
    return {
      city: "",
    };
  },
  methods: {
    emitWeather() {
      this.$emit("city", this.city);
    },
  },
};
</script>

<style scoped lang="scss">
.CityInput {
  margin: 1rem 0;

  &__btn,
  &__input {
    border-radius: 1rem;
    padding: .5rem 1rem;
  }

  &__btn {
    background-color: black;
    color: white;
    font-weight: 700;
    margin-left: 1rem;
  }

  &__input {
    text-align: center;
    font-weight: 700;
  }
}
</style>
