<script setup>
import { onMounted, ref } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import NavBar from './components/NavBar.vue'
import '../fontawesome-free-6.7.2-web/js/all.js'

const showButton = ref(false)

const checkScroll = () => {
  showButton.value = window.scrollY > 300
}

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  })
}

onMounted(() => {
  window.addEventListener('scroll', checkScroll)
  return () => {
    window.removeEventListener('scroll', checkScroll)
  }
})
</script>

<template>
  <NavBar />
  <main class="content">
    <RouterView />
  </main>
  <button 
    v-if="showButton" 
    @click="scrollToTop" 
    class="back-to-top"
    aria-label="Back to top"
  >
    <i class="fas fa-arrow-up"></i>
  </button>
</template>   

<style scoped>
@import url('../fontawesome-free-6.7.2-web/css/all.min.css'); 

.back-to-top {
  position: fixed;
  bottom: 2rem;
  right: 2rem;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: #4a6cf7;
  color: white;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
  transition: all 0.3s ease;
  z-index: 1000;
  opacity: 0.9;
}

.back-to-top:hover {
  background-color: #3a5bd9;
  transform: translateY(-3px);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
}

.back-to-top:active {
  transform: translateY(0);
}
</style>

<!-- Global styles (not scoped) to enhance scrolling behavior -->
<style>
:root { --header-offset: 72px; }
html { scroll-behavior: smooth; }
/* Ensure in-page anchors are not hidden under the fixed header */
section[id] { scroll-margin-top: var(--header-offset); }
</style>
