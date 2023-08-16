<template>
  <div>
    <section class="text-3 flex justify-center content-center flex-col mx-auto text-center"></section>
    <section class="flex text-6xl justify-center content-center">
      <div class="days mr-2 relative">
        {{ displayDays }}
        <div class="label text-sm absolute bottom-0"> Days</div>
      </div>
    </section>
  </div>
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
