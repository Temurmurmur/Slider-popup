<template>
  <div class="carousel">
      <slot></slot>

    <button @click="next" class="btn btn-next"><img src="../../assets/img/arr-next.svg" alt=""></button>
    <button @click="prev" class="btn btn-prev"><img src="../../assets/img/arr-prev.svg" alt=""></button>
  </div>
</template>

<script>
  export default {
    methods: {
      next() {
        this.$emit('next')
      },
      prev() {
        this.$emit('prev')
      }
    }
  }
</script>

<style scoped>

</style>