<template>
  <div class="about">
    <h1>This is an about page</h1>
    <Animateion :number="value" :time="10" :step="1" />
  </div>
</template>

<script>
import Vue from 'vue'
import Animateion from '../components/Animateion.vue';
Vue.component(Animateion)

export default {
  data() {
    return {
      value: 0
    }
  },
  components: {Animateion},
  mounted() {
    setTimeout(() => {
      this.value = 100
      console.log('value is : ', this.value)
    }, 2000)
  }
}

</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
