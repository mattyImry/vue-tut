<template>
  <div>
    <button @click.prevent="reset">start</button>
    <button @click.prevent="setPresetTimer(10)">10 seconds</button>
    <button @click.prevent="setPresetTimer(10 * 60)">10 Minutes</button>
    <button @click.prevent="setPresetTimer(30 * 60)">30 Minutes</button>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue'

const emit = defineEmits(['sendPreset', 'reset'])

const { end } = defineProps(['end'])
const presetEnd = ref(end)

function setPresetTimer(seconds) {
  const now = new Date()
  const newEndTime = new Date(now.getTime() + seconds * 1000)
  presetEnd.value = newEndTime
  emit('sendPreset', newEndTime)
}
function reset() {
  emit('reset')
}
</script>

<style></style>
