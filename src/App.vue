<template>
  <div id="app">
    <Formulario />
    <Usuarios />

  </div>
</template>

<script>
import Formulario from './components/Formulario.vue'
import Usuarios from './components/Usuarios.vue'

export default {
  name: 'App',
  components: {
    Formulario,
    Usuarios,
  }
}
</script>

<style>

</style>
