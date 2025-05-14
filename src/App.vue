<!-- App.vue -->
<script setup>
import { RouterView, RouterLink } from 'vue-router'
import Navbar from './components/Header.vue'
import Ood from './components/podval.vue'

</script>

<template>
  <div id="app">
    <Navbar />
    <RouterView />
    <Ood/>
   
  </div>
</template>

<style scoped>
/* если есть стили */
</style>