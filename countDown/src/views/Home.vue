<template>
  <div class="comps">
    <Counter />
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
