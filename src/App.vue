<template>
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <AltasBajas></AltasBajas>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import AltasBajas from './components/AltasBajasCambios.vue'

export default {
  name: 'App',
  components: {
    AltasBajas
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
  margin-top: 60px;
}
</style>
