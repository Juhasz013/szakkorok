<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>
    <div>
      <nav>
        <RouterLink to="/"></RouterLink>
      </nav>
    </div>
  </header>
 <RouterView/>
</template>

<style scoped>

</style>
