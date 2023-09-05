<template>
  <h1>Count Down</h1>
  <div class="inputs">
    <label for="year">Year: </label>
    <input type="number" v-model="data.year" />

    <label for="month">Month: </label>
    <input type="number" v-model="data.month" min="1" max="12" />

    <label for="date">Date: </label>
    <input type="number" v-model="data.date" min="1" max="31" />

    <label for="hour">Hour: </label>
    <input type="number" v-model="data.hour" min="0" max="23" />

    <label for="minute">Minutes: </label>
    <input type="number" v-model="data.minute" min="0" max="60" />

    <label for="second">Seconds: </label>
    <input type="number" v-model="data.second" min="0" max="60" />
  </div>
  <div class="comps">
    <Counter
      :year="data.year"
      :month="data.month"
      :date="data.date"
      :hour="data.hour"
      :minute="data.minute"
      :second="data.second"
      :millisecond="0"
    />
  </div>
</template>
<script setup lang="ts">
import Counter from '@/components/Counter.vue'
import { ref } from 'vue'

interface DatesInput {
  year: number
  month: number
  date: number
  hour: number
  minute: number
  second: number
  millisecond: number
}

const data = ref<DatesInput>({
  year: 2023,
  month: 12,
  date: 9,
  hour: 1,
  minute: 10,
  second: 10,
  millisecond: 10
})
</script>
<style lang="css" scoped>
h1 {
  margin-bottom: 1rem;
}
.comps {
  text-align: center;
}

.inputs {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
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
