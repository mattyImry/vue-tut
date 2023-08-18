<template>
  <div class="comps">
    <Counter
      :year="2023"
      :month="7"
      :date="18"
      :hour="11"
      :minute="30"
      :second="22"
      :millisecond="11"
    />
  </div>
</template>
<script>
import Counter from '@/components/Counter.vue'
export default {
  components: {
    Counter
  }
}
</script>
<style lang="css" scoped>
.comps {
  display: flex;
  text-align: center;
}
</style>
