<template>
  <div class="animate-elements-container">
    <slot></slot>
  </div>
</template>

<script>
import { gsap } from 'gsap';

export default {
  name: 'AnimateElements',
  props: {
    delay: {
      type: Number,
      default: 0,
    },
    staggerDelay: {
      type: Number,
      default: 0.2,
    },
  },
  mounted() {
    this.animateElements();
  },
  methods: {
    animateElements() {
      const elements = this.$el.children;

      gsap.set(elements, { autoAlpha: 0, y: 40 });

      gsap.to(elements, {
        autoAlpha: 1,
        y: 0,
        duration: 0.5,
        delay: this.delay,
        stagger: this.staggerDelay,
        ease: 'power3.out',
      });
    },
  },
};
</script>

<style>
.animate-elements-container {
    width: 100%;
    display: flex;
}
</style>