<template>
  <q-page class="flex flex-center flex-column">
    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-vertical.svg"
      style="width: 200px; height: 200px"
    >
    <router-link to="/Inicio" class="button-web " >
      iniciar 
    </router-link>
  </q-page>
 
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage'
})
</script>
