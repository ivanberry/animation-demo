<template>
    <div>

    <button @click="create">CREATE</button>
    <main class="flex">
        <section class="flex-item" v-for="item in els" :key="item">
            {{ item }}
        </section>
    </main>
    </div>
</template>

<script>
import Vue from 'vue'
import { gsap } from 'gsap';
import AnimateMultiple from '../components/AnimateMultiple.vue';

Vue.component(AnimateMultiple)

export default {
    components: {
        AnimateMultiple
    },
  data() {
    return {
      number: 0,
      els: []
    }
  },
  methods: {
    create() {
        this.els = []
        this.els = Array.from('asdfge')
        this.animateStagger('.flex-item')
    },
    animateStagger(selector, options = {}) {
        const defaultOptions = {
          delay: 0,
          staggerDelay: 0.2,
          duration: 0.5,
          ease: 'power3.out',
        };

        const mergedOptions = { ...defaultOptions, ...options };
        const elements = document.querySelectorAll(selector);

        gsap.set(elements, { autoAlpha: 0, y: 40, scale: 1.5 });

        gsap.to(elements, {
          autoAlpha: 1,
          y: 0,
          scale: 1,
          duration: mergedOptions.duration,
          delay: mergedOptions.delay,
          stagger: mergedOptions.staggerDelay,
          ease: mergedOptions.ease,
        });
    }
  },
  mounted() {
    setTimeout(() => {
        this.els = Array.from('1234')
        this.$nextTick(() => {
            this.animateStagger('.flex-item')
        })
    }, 2000)
  }
}

</script>

<style scoped>
    .flex {
        display: flex;
        justify-content: space-between;
        border: 1px solid red;
        height: 300px;
    }

    .flex-item {
        flex: 1;
        border: 1px solid green;
        text-align: center;
    }
</style>