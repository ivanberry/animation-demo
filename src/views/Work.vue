<template>
    <div class="container">
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
        this.$nextTick(() => {
            this.animateStaggerMore('.flex-item')
        })
    },
    animateStagger(selector, options = {}) {
        const defaultOptions = {
          delay: 0,
          staggerDelay: 0.2,
          duration: 0.5,
        //   ease: 'power3.out',
          ease: 'bounce.out'
        };

        const mergedOptions = { ...defaultOptions, ...options };
        const elements = document.querySelectorAll(selector);

        gsap.set(elements, { autoAlpha: 0, y: -200 });

        gsap.to(elements, {
          autoAlpha: 1,
          y: 0,
          duration: mergedOptions.duration,
          delay: mergedOptions.delay,
          stagger: mergedOptions.staggerDelay,
          ease: mergedOptions.ease,
        });
    },
    animateStaggerMore(selector, options = {}) {
  const defaultOptions = {
    delay: 0,
    staggerDelay: 0.4,
    duration: 1.5,
    ease: 'bounce.out',
  };

  const mergedOptions = { ...defaultOptions, ...options };
  const elements = document.querySelectorAll(selector);

  gsap.set(elements, { 
    autoAlpha: 0, 
    y: -100, 
    position: 'fixed', 
    top: '50%', 
    left: '50%',
    transform: 'translate(-50%, -50%)'
  });

  const masterTimeline = gsap.timeline({ delay: mergedOptions.delay });

  elements.forEach((element) => {
    const timeline = gsap.timeline();

    timeline
      .to(element, {
        autoAlpha: 1,
        y: '50%',
        duration: mergedOptions.duration * 0.5,
        ease: mergedOptions.ease,
        scaleY: 1.2,
      })
      .to(element, {
        rotationY: 180,
        duration: mergedOptions.duration * 0.5,
        ease: 'power1.inOut',
      })
      .to(element, {
        y: 0,
        scaleY: 1,
        duration: mergedOptions.duration * 0.5,
        ease: 'power3.out',
        onComplete: () => {
          gsap.set(element, { clearProps: 'all' });
        },
      });

    masterTimeline.add(timeline, '+=0.4'); // Add each timeline to the master timeline with a stagger delay
  });
}
  },
  mounted() {
    setTimeout(() => {
        this.els = Array.from('1234')
        this.$nextTick(() => {
            this.animateStaggerMore('.flex-item')
        })
    }, 2000)
  }
}

</script>

<style scoped>
    .container {
        position: relative;
    }

    .flex {
        display: flex;
        justify-content: space-between;
        border: 1px solid red;
        height: 300px;
    }

    .flex-item {
        flex: 0 0 300px;
        border: 1px solid green;
        text-align: center;
    }
</style>