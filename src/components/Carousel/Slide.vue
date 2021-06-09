<template>
  <transition :name="direction" mode="in-out">
    <div v-show="curent === visibleSlide" class="slide">
      <slot></slot>
    </div>
  </transition>
</template>

<script>
  export default {
    props: ['curent', 'visibleSlide', 'direction'],
    data() {
      return {
        index: 0,
      }
    },
    computed: {}
  }
</script>

<style lang="scss">
  /*.slide{*/
  /*  position: absolute;*/
  /*  left: 0;*/
  /*  bottom: 0;*/
  /*  top: 0;*/
  /*  right: 0;*/
  /*}*/
  .left-enter-active {
    animation: left-in 0.5s ease-in;
  }

  .left-leave-active {
    animation: left-out 0.5s ease-in;
  }

  @keyframes left-out {
    from {
      transform: translateX(0%);
    }
    to {
      transform: translateX(-100%);
    }
  }

  @keyframes left-in {
    from {
      transform: translateX(100%);
    }
    to {
      transform: translateX(0);
    }
  }

  .right-enter-active {
    animation: right-in 0.5s ease-in;
  }

  .right-leave-active {
    animation: right-out 0.5s ease-in;
  }

  @keyframes right-in {
    from {
      transform: translateX(-100%);
    }
    to {
      transform: translateX(0);
    }
  }

  @keyframes right-out {
    from {
      transform: translateX(0%);
    }
    to {
      transform: translateX(100%);
    }
  }


</style>