<template>
  <div>
    <button @click.prevent="reset">start</button>
    <button @click.prevent="setPresetTimer(10)">10 seconds</button>
    <button @click.prevent="setPresetTimer(10 * 60)">10 Minutes</button>
    <button @click.prevent="setPresetTimer(30 * 60)">30 Minutes</button>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

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

<style></style>
