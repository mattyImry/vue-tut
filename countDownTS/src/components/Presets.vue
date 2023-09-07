<template>
  <div>
    <button @click.prevent="reset()">Start Timer</button>
    <button @click.prevent="setPresetTimer(10)">10 seconds</button>
    <button @click.prevent="setPresetTimer(10 * 60)">10 Minutes</button>
    <button @click.prevent="setPresetTimer(30 * 60)">30 Minutes</button>
  </div>
  <div class="input-user">
    <h3>Set your timer</h3>

    <label for="hour">Minutes: </label>
    <input type="number" name="minutes" v-model="inputTime" />
    <button @click.prevent="setPresetTimer(inputTime * 60)">Set Timer</button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const inputTime = ref(0)

const emit = defineEmits<{ sendPreset: [newEndTime: Date]; reset: [] }>()

const presetEnd = ref<Date | null>(null)

function setPresetTimer(seconds: number): void {
  const now = new Date()
  const newEndTime = new Date(now.getTime() + seconds * 1000)
  presetEnd.value = newEndTime

  //to parent comp
  emit('sendPreset', newEndTime)
}

function reset(): void {
  presetEnd.value = null
  emit('reset')
}
</script>

<style>
.input-user {
  margin-top: 20px;
}

.input-user h3 {
  font-weight: 500;
}
</style>
