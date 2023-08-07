<script setup lang="ts">
import { ref, watchEffect } from 'vue'

interface WeatherData {
  name: string
  main: {
    temp: number
  }
  weather: [
    {
      main: string
    }
  ]
}

let query = ref('London')
const weather = ref<WeatherData | null>(null)

let d: Date = new Date()
let months: string[] = [
  'January',
  'February',
  'March',
  'April',
  'May',
  'June',
  'July',
  'August',
  'September',
  'October',
  'November',
  'December'
]
let days: string[] = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']
let day: string = days[d.getDay()]
let date: number = d.getDate()
let month: string = months[d.getMonth()]
let year: number = d.getFullYear()

watchEffect(async () => {
  try {
    const response = await fetch(
      `http://api.openweathermap.org/data/2.5/weather?q=${query.value}&units=metric&id=524901&appid=7cc399b56538bbe7b6574e4860bb0802`
    )
    const data = await response.json()
    weather.value = data
  } catch (error) {
    console.error('Error fetching weather data:', error)
  }
})
</script>

<template>
  <main>
    <div class="search-box">
      <form action="">
        <input
          type="text"
          name="search-box"
          id="search-box"
          class="search-bar"
          placeholder="Search"
          v-model="query"
        />
      </form>
    </div>
    <div class="weather-wrap">
      <div class="location-box">
        <div class="location">{{ weather!.name }}</div>
        <div class="date">{{ day }} {{ date }} {{ month }} {{ year }}</div>
        <div class="weather-box">
          <div class="temp">{{ Math.floor(weather!.main.temp) }}C</div>
          <div class="weather">{{ weather!.weather[0].main }}</div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  color: #313131;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
.search-box .search-bar:focus {
  background-color: rgba(255, 255, 255, 0.75);
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  border-radius: 16px 0px 16px 0px;
}

.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
