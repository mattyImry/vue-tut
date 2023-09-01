<template>
  <div>
    <button @click="showRemaining">start</button>
    <button @click="setPresetTimer(10)">10 seconds</button>
    <button @click="setPresetTimer(10 * 60)">10 Minutes</button>
    <button @click="setPresetTimer(30 * 60)">30 Minutes</button>
  </div>
</template>

<script setup>
const props = defineProps('end')

function setPresetTimer(seconds) {
  let endTimer = props.end
  const now = new Date()
  const newEndTime = new Date(now.getTime() + seconds * 1000)
  endTimer = newEndTime
  showRemaining()
}
</script>

<style></style>
