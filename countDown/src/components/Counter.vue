<template>
  <div>{{ displayDays }}{{ displayHours }}{{ displayMinutes }}{{ displaySeconds }}</div>
</template>

<script>
export default {
  data: () => ({
    displayDays: 0,
    displayHours: 0,
    displayMinutes: 0,
    displaySeconds: 0
  })
}
</script>

<style lang="scss" scoped></style>
