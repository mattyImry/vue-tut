<template>
  <div class="container" v-if="loaded">
    <h3 v-if="!running">Counting</h3>
    <h3 v-else>Count Down Completed</h3>

    <section>
      <div class="semi">
        {{ displayDays }}
        <div class="">Days</div>
      </div>
      <div class="semi">
        {{ displayHours }}
        <div class="">Hours</div>
      </div>
      <div class="semi">
        {{ displayMinutes }}
        <div class="">Minutes</div>
      </div>
      <div class="semi">
        {{ displaySeconds }}
        <div class="">Seconds</div>
      </div>
    </section>

    <Presets :end="end" @sendPreset="handlePresets" @reset="handleReset" />
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import Presets from './Presets.vue'

const props = defineProps(['year', 'month', 'date', 'hour', 'minute', 'second', 'millisecond'])

const dateFromChild = ref(0)

const displayDays = ref(0)
const displayHours = ref(0)
const displayMinutes = ref(0)
const displaySeconds = ref(0)
const loaded = ref(false)
const running = ref(false)

const _seconds = 1000
const _minutes = computed(() => _seconds * 60)
const _hours = computed(() => _minutes.value * 60)
const _days = computed(() => _hours.value * 24)

const end = ref(
  new Date(
    props.year,
    props.month - 1,
    props.date,
    props.hour,
    props.minute,
    props.second,
    props.millisecond
  )
)

const formatNum = (num) => (num < 10 ? '0' + num : num)
let timer

const showRemaining = () => {
  clearInterval(timer)
  timer = setInterval(() => {
    const now = new Date()
    const distance = end.value.getTime() - now.getTime()
    running.value = false

    if (distance < 0) {
      clearInterval(timer)
      running.value = true
      loaded.value = true
      displayMinutes.value = 0
      displaySeconds.value = 0
      displayHours.value = 0
      displayDays.value = 0
      return
    }

    const days = Math.floor(distance / _days.value)
    const hours = Math.floor((distance % _days.value) / _hours.value)
    const minutes = Math.floor((distance % _hours.value) / _minutes.value)
    const seconds = Math.floor((distance % _minutes.value) / _seconds)
    displayMinutes.value = formatNum(minutes)
    displaySeconds.value = formatNum(seconds)
    displayHours.value = formatNum(hours)
    displayDays.value = formatNum(days)
    loaded.value = true
  })
}

function handlePresets(dateFromChild) {
  // dateFromChild.value = newEndTime
  end.value = dateFromChild
  clearInterval(timer) // Clear the previous timer
  showRemaining() // Start a new timer with the updated end time
}

function handleReset() {
  console.log('parent')
  clearInterval(timer) // Clear the previous timer
  showRemaining() // Start a new timer with the updated end time
  // showRemaining(end.value)
}

onMounted(showRemaining)
</script>

<style lang="css" scoped>
section {
  display: flex;
  text-align: center;
}

.semi {
  margin-left: 20px;
}
</style>
