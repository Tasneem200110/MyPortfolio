<script setup>
import { RouterLink, RouterView } from 'vue-router'
import NavBar from './components/NavBar.vue'
import '../fontawesome-free-6.7.2-web/js/all.js'
</script>

<template>
  <NavBar />
  <main class="content">
    <RouterView />
  </main>
</template>   

<style scoped>
@import url('../fontawesome-free-6.7.2-web/css/all.min.css'); 
</style>

<!-- Global styles (not scoped) to enhance scrolling behavior -->
<style>
:root { --header-offset: 72px; }
html { scroll-behavior: smooth; }
/* Ensure in-page anchors are not hidden under the fixed header */
section[id] { scroll-margin-top: var(--header-offset); }
</style>
