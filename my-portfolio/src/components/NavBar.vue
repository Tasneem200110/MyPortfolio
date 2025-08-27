<template>
  <header class="navbar" :class="{ 'fixed-nav': isScrolled }" role="banner">
    <div class="navbar-spacer" v-if="!isScrolled"></div>
    <nav class="nav-inner" aria-label="Main Navigation">
      <div class="left">
        <a href="#" class="logo" aria-hidden="true">
          <img src="../assets/logo7.png" alt="Logo" class="logo-img" />
        </a>
      </div>

      <!-- Mobile menu button -->
      <button 
        class="mobile-menu-button" 
        @click="toggleMobileMenu"
        :aria-expanded="isMenuOpen ? 'true' : 'false'"
        aria-label="Toggle menu"
      >
        <i :class="isMenuOpen ? 'fas fa-times' : 'fas fa-bars'"></i>
      </button>

      <div class="nav-links" :class="{ 'mobile-visible': isMenuOpen }">
        <ul class="center">
          <li>
            <a
              href="#about"
              @click="navClick('about')"
              :class="{ active: activeSection === 'about' }"
              :aria-current="activeSection === 'about' ? 'page' : null"
              class="nav-link"
            >About Me</a>
          </li>
          <li>
            <a
              href="#skills"
              @click="navClick('skills')"
              :class="{ active: activeSection === 'skills' }"
              :aria-current="activeSection === 'skills' ? 'page' : null"
              class="nav-link"
            >Skills</a>
          </li>
          <li>
            <a
              href="#projects"
              @click="navClick('projects')"
              :class="{ active: activeSection === 'projects' }"
              :aria-current="activeSection === 'projects' ? 'page' : null"
              class="nav-link"
            >Projects</a>
          </li>
          <li>
            <a
              href="#contact"
              @click="navClick('contact')"
              :class="{ active: activeSection === 'contact' }"
              :aria-current="activeSection === 'contact' ? 'page' : null"
              class="nav-link"
            >Contact Me</a>
          </li>
        </ul>

      </div>
      <div class="right">
        <a class="resume nav-link" :href="resumeHref" target="_blank" download @click="closeMenu">
          <span>Resume</span>
          <i class="fa-solid fa-file-arrow-down"></i>
        </a>
      </div>
    </nav>
  </header>
  <div class="navbar-spacer" aria-hidden="true"></div>
  
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick, watch } from 'vue'

const resumeHref = 'https://drive.google.com/file/d/1T8ulVB2Pynezx6hQHRYrbnYH0BuiMAC7/view?usp=sharing'

const sectionIds = ['about','skills','projects','contact']
const activeSection = ref('')
const isMenuOpen = ref(false)
const isMobile = ref(window.innerWidth < 1024)
const isScrolled = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 10
}

// Toggle mobile menu
const toggleMobileMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
  document.body.style.overflow = isMenuOpen.value ? 'hidden' : ''
}

// Close menu when clicking outside
const handleClickOutside = (event) => {
  const navElement = document.querySelector('.nav-inner')
  const button = document.querySelector('.mobile-menu-button')
  if (navElement && !navElement.contains(event.target) && !button.contains(event.target) && isMenuOpen.value) {
    closeMenu()
  }
}

// Close menu and handle click
const navClick = (section) => {
  scrollToId(section)
  closeMenu()
}

// Close menu helper
const closeMenu = () => {
  isMenuOpen.value = false
  document.body.style.overflow = ''
}

// Handle window resize
const handleResize = () => {
  isMobile.value = window.innerWidth < 1024
  if (!isMobile.value) {
    closeMenu()
  }
}

function getHeaderOffset() {
  const nav = document.querySelector('.navbar')
  return nav ? Math.ceil(nav.getBoundingClientRect().height) : 72
}

function scrollToId(id) {
  const el = document.getElementById(id)
  if (!el) return
  const headerOffset = getHeaderOffset()
  const elementPosition = el.getBoundingClientRect().top + window.pageYOffset
  const offsetPosition = elementPosition - headerOffset
  window.scrollTo({ top: offsetPosition, behavior: 'smooth' })
}

function updateActive() {
  const headerOffset = getHeaderOffset()
  let current = ''
  let bestDelta = Number.POSITIVE_INFINITY
  for (const id of sectionIds) {
    const el = document.getElementById(id)
    if (!el) continue
    const rectTop = el.getBoundingClientRect().top
    const delta = Math.abs(rectTop - headerOffset)
    if (rectTop <= headerOffset + 10 && delta < bestDelta) {
      bestDelta = delta
      current = id
    }
  }
  activeSection.value = current
}

// Initialize event handlers
const onScroll = () => updateActive()
const onResizeHandler = () => {
  handleResize()
  updateActive()
}

onMounted(async () => {
  await nextTick()
  updateActive()
  window.addEventListener('scroll', handleScroll)
  
  // Add event listeners
  window.addEventListener('scroll', onScroll, { passive: true })
  window.addEventListener('resize', onResizeHandler)
  document.addEventListener('click', handleClickOutside)

  // Handle hash on initial load/refresh
  const hash = window.location.hash?.replace('#','')
  if (hash && sectionIds.includes(hash)) {
    // slight delay to ensure layout settled
    setTimeout(() => scrollToId(hash), 50)
  }
})

onBeforeUnmount(() => {
  // Clean up event listeners
  window.removeEventListener('scroll', onScroll)
  window.removeEventListener('resize', onResizeHandler)
  window.removeEventListener('scroll', handleScroll)
  document.removeEventListener('click', handleClickOutside)
  
  // Reset body overflow
  document.body.style.overflow = ''
  
  // Reset menu state
  isMenuOpen.value = false
})

</script>

<style scoped>
.navbar {
  width: 100%;
  background: white;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  position: relative;
  z-index: 1000;
  transition: all 0.3s ease;
}

.navbar.fixed-nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  animation: slideDown 0.3s ease-out;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

@keyframes slideDown {
  from { transform: translateY(-100%); }
  to { transform: translateY(0); }
}

.navbar-spacer {
  transition: height 0.3s ease;
}

.nav-inner {
  margin: 0 120px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: relative;
}

/* Mobile menu button */
.mobile-menu-button {
  display: none;
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  z-index: 1001;
  color: #0b0b0b;
  transition: transform 0.2s ease;
  position: absolute;
  right: 0px;
  top: 50%;
  transform: translateY(-50%);
}

.mobile-menu-button:active {
  transform: scale(0.95);
}

/* Logo */
.left {
  display: flex;
  align-items: center;
  z-index: 1001;
}

.logo {
  display: inline-flex;
  width: 130px;
  height: 40px;
  transition: transform 0.3s ease;
}

.logo:hover {
  transform: scale(1.03);
}

.logo-img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  display: block;
}

/* Navigation links container */
.nav-links {
  display: flex;
  align-items: center;
  gap: 32px;
  height: 100%;
}

/* Mobile menu styles */
@media (max-width: 1023px) {
  .navbar{
    margin: 0;
    padding: 0;
    position: relative;
  }
  .nav-inner {
    margin: 0;
    padding: 0;
    position: relative;
  }
  .mobile-menu-button {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 40px;
    height: 40px;
    background: transparent;
    border: none;
    cursor: pointer;
    z-index: 1001;
    padding: 0;
    color: #4b4b4b;
    font-size: 24px;
  }
  .nav-links {
    position: fixed;
    top: 0;
    right: -280px;
    width: 200px;
    height: 100vh;
    background: white;
    flex-direction: column;
    justify-content: flex-start;
    padding: 80px 25px 30px;
    box-shadow: -5px 0 30px rgba(0, 0, 0, 0.1);
    transition: right 0.3s ease-in-out;
    z-index: 1000;
    overflow-y: auto;
    display: flex;
    align-items: flex-start;
    gap: 20px;
    opacity: 0;
    pointer-events: none;
  }
  
  .nav-links.mobile-visible {
    right: 0;
    opacity: 1;
    pointer-events: auto;
  }
  
  .nav-links.mobile-visible {
    right: 0;
  }
  
  .center {
    flex-direction: column;
    width: 100%;
    gap: 15px;
    list-style: none;
    padding: 0;
    margin: 0 0 20px 0;
    display: flex !important;
  }
  
  .center li {
    width: 100%;
    border-bottom: 1px solid #f0f0f0;
  }
  
  .center li:last-child {
    border-bottom: none;
  }
  
  .center a {
    display: block;
    padding: 12px 0;
    font-size: 16px;
    color: #9ca3af;
    text-decoration: none;
    transition: all 0.2s;
    position: relative;
    font-size: 1rem;
    font-weight: 400;
    display: inline-block;
    padding: 8px 12px;
    border-radius: 4px;
  }
  
  .center a:hover,
  .center a.active {
    color: #0b0b0b;
    font-weight: 500;
  }
  
  .right {
    width: 100%;
  }
  
  .resume {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    padding: 8px 16px;
    background: #3b82f6;
    color: white;
    font-weight: 500;
    border-radius: 4px;
    transition: all 0.3s ease;
    text-decoration: none;
    width: auto;
    margin: 0 auto;
  }
  
  .resume:hover {
    background: #2563eb;
    transform: translateY(-1px);
  }
  
  .resume i {
    font-size: 0.9em;
    color: inherit;
  }
}

.center {
  display: flex;
  list-style: none;
  gap: 24px;
  padding: 0;
  margin: 0;
}

.center a {
  text-decoration: none;
  transition: all 0.2s;
  position: relative;
  font-size: 1rem;
  font-weight: 400;
  display: inline-block;
  padding: 8px 12px;
  border-radius: 4px;
}

.center a:hover,
.center a.active {
  color: #0b0b0b;
  font-weight: 500;
}

.nav-link {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 12px;
  border-radius: 4px;
  transition: all 0.3s ease;
}

.nav-link:hover {
  background-color: rgba(255, 255, 255, 0.1);
}

.center a.active {
  color: #181818;
  font-weight: 500;
}

.center a::after {
  content: "";
  position: absolute;
  left: 0;
  bottom: 4px;
  width: 100%;
  height: 2px;
  background: #0b0b0b;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.3s ease;
  border-radius: 2px;
}

.center a:hover::after,
.center a.active::after {
  transform: scaleX(1);
}

/* Tablet styles */
@media (max-width: 1023px) {
  .center a {
    font-size: 16px;
    padding: 10px 0;
    width: 100%;
    text-align: center;
  }
  
  .center a::after {
    bottom: 0;
    left: 50%;
    width: 30px;
    transform: translateX(-50%) scaleX(0);
    transform-origin: center;
  }
  
  .center a.active::after,
  .center a:hover::after {
    transform: translateX(-50%) scaleX(1);
  }
}

.right {
  display: flex;
  justify-content: center;
}

.resume {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  color: #fff;
  background: #0b0b0b;
  border: none;
  border-radius: 8px;
  padding: 10px 10px;
  font-size: 14.5px;
  font-weight: 400;
  text-decoration: none;
  cursor: pointer;
  transition: all 0.2s ease;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  position: relative;
  overflow: hidden;
  z-index: 1;
  width: auto;
  height: auto;
}

.resume::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: auto;
  height: auto;
  background: linear-gradient(45deg, #111, #333);
  z-index: -1;
  transition: opacity 0.3s ease;
  opacity: 1;
}

.resume:hover::before {
  opacity: 0.9;
}

.resume:active {
  transform: translateY(1px);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.resume i {
  font-size: 0.9em;
  transition: transform 0.2s ease;
}

.resume:hover i {
  transform: translateY(-1px);
}

.resume:hover {
  opacity: 1;
  transform: translateY(-2px);
  background: linear-gradient(180deg, #161616 0%, #616161 100%);
  box-shadow: 0 10px 28px rgba(0,0,0,0.18), 0 0 0 3px rgba(235,151,168,0.25) inset;
  border-color: rgba(175, 168, 168, 0.18);
}

.resume:focus-visible { outline: 2px solid #000; outline-offset: 3px; }
.icon { opacity: 0.95; }

@media (max-width: 800px) {
  .center { display: none; }
  .nav-inner { padding: 0 16px; }
  .logo { width: 120px; }
}
</style>
