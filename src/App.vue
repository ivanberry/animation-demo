<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div id="app">
    <header>
      <div class="wrapper">
        <nav>
          <router-link to="/">Home</router-link>
          <router-link to="/about">About</router-link>
          <router-link to="/work">Work</router-link>
        </nav>
      </div>
    </header>
    <transition
      :name="transition"
      mode="in-out"
    >
      <router-view />
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      transition: ''
    }
  },
  watch: {
    $route(to) {
      if (to.meta.animate) {
        this.transition = 'slide-fade'
      } else {
        this.transition = ''
      }
    }
  }
}
</script>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  /* transform: translateX(10px); */
  opacity: 0;
}
</style>
