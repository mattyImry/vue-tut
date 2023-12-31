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

    <Presets @sendPreset="handlePresets" @reset="handleReset" />
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, watchEffect } from 'vue'
import Presets from './Presets.vue'

import type { DatesInput } from '../views/Home.vue'

const props = defineProps<DatesInput>()

const displayDays = ref<number>(0)
const displayHours = ref<number>(0)
const displayMinutes = ref<number>(0)
const displaySeconds = ref<number>(0)
const loaded = ref<boolean>(false)
const running = ref<boolean>(false)

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

watchEffect(() => {
  // Update the 'end' ref with new input values
  end.value = new Date(
    props.year,
    props.month - 1,
    props.date,
    props.hour,
    props.minute,
    props.second,
    props.millisecond
  )
})

const formatNum = (num: number): number => (num < 10 ? 0 + num : num)

const showRemaining = (): void => {
  const timer = setInterval(() => {
    const now: Date = new Date()
    const distance: number = end.value.getTime() - now.getTime()
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

function handlePresets(dateFromChild: Date): void {
  end.value = dateFromChild
  showRemaining()
}

function handleReset(): void {
  showRemaining()
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

.container h3 {
  font-weight: 500;
}
</style>
