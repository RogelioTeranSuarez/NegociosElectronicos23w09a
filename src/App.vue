<template>
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
  </head>

  <body class="body">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div>
      <AltasBajas></AltasBajas>
    </div>
  </body>

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
  background-color: #363636;
}

/* Establecer un color de fondo */
body {
  background-color: #363636;
  height: 100%;
  margin: 0;
  padding: 0;
}
</style>
