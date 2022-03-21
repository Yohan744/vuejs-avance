<template>
  <HomeStore/>
</template>

<script>
import HomeStore from './components/Home.vue'

export default {
  name: 'App',
  components: {
    HomeStore
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
