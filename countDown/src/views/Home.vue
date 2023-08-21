<template>
  <div class="inputs">
    <label for="year">Year: </label>
    <input type="number" v-model="year" />

    <label for="month">Month: </label>
    <input type="number" v-model="month" />

    <label for="date">Date: </label>
    <input type="number" v-model="date" />

    <label for="hour">Hour: </label>
    <input type="number" v-model="hour" />

    <label for="minute">Minutes: </label>
    <input type="number" v-model="minute" />

    <label for="second">Seconds: </label>
    <input type="number" v-model="second" />
  </div>
  <div class="comps">
    <Counter
      :year="year"
      :month="month"
      :date="date"
      :hour="hour"
      :minute="minute"
      :second="second"
      :millisecond="0"
    />
  </div>

  <div class="pre-sets"></div>
</template>
<script>
import Counter from '@/components/Counter.vue'

export default {
  components: {
    Counter
  },

  data() {
    return {
      year: 2025,
      month: 5,
      date: 22,
      hour: 10,
      minute: 55,
      second: 22,
      millisecond: 11
    }
  }
}
</script>
<style lang="css" scoped>
.comps {
  text-align: center;
}

.inputs {
  display: grid;
  grid-template-columns: 1fr 1fr;
  text-align: center;
}

input {
  width: 4rem;
  margin-bottom: 1rem;
  margin-left: 0.5rem;
  text-align: center;
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}

label {
  font-weight: bold;
}
</style>
