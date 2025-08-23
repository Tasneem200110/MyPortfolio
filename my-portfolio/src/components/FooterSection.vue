<template>
  <footer class="site-footer" :class="themeClass">
    <div class="footer-inner">
      <img class="logo" :class="logoClass" src="../assets/logo7.png" alt="Logo" />
      <a class="email" :href="`mailto:${email}`">{{ email }}</a>
    </div>
  </footer>
  
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  email: { type: String, default: 'tasneemmostafa200110@gmail.com' },
  // theme: 'dark' (black bg) or 'light'
  theme: { type: String, default: 'dark' },
  // If true and theme is dark, force the logo to a light variant via CSS filter
  invertLogoOnDark: { type: Boolean, default: true }
})

const email = computed(() => props.email?.trim())
const themeClass = computed(() => props.theme === 'dark' ? 'is-dark' : 'is-light')
const logoClass = computed(() => (props.theme === 'dark' && props.invertLogoOnDark) ? 'logo-invert' : '')
</script>

<style scoped>
.site-footer {
  color: #fff;
  padding: 2.5rem 0;
  width: 100%;
  position: relative;
  overflow: hidden;
}

.site-footer.is-dark { 
  background: #000; 
}

.site-footer.is-light { 
  background: #f5f5f5; 
  color: #111; 
}

.footer-inner {
  width: 90%;
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  gap: 1.5rem;
  align-items: center;
  justify-content: space-between;
  padding: 0 1rem;
}

.logo { 
  height: 2.25rem; 
  width: auto; 
  object-fit: contain; 
  display: block; 
  transition: filter 0.3s ease, opacity 0.3s ease;
}

.logo-invert { 
  filter: brightness(0) invert(1) contrast(1.05); 
}

.email { 
  color: inherit; 
  text-decoration: none; 
  font-weight: 600;
  font-size: clamp(0.9rem, 1.5vw, 1rem);
  transition: opacity 0.3s ease, transform 0.3s ease;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 100%;
}

.email:hover { 
  opacity: 0.85;
  text-decoration: none;
  transform: translateY(-1px);
}

/* Responsive Adjustments */
@media (max-width: 1024px) {
  .footer-inner {
    width: 90%;
    padding: 0 1.5rem;
  }
}

@media (max-width: 768px) {
  .site-footer {
    padding: 2rem 0;
  }
  
  .footer-inner {
    flex-direction: column;
    gap: 1.25rem;
    text-align: center;
  }
  
  .logo {
    margin-bottom: 0.5rem;
  }
  
  .email {
    font-size: 1rem;
    white-space: normal;
    text-align: center;
  }
}

@media (max-width: 480px) {
  .site-footer {
    padding: 1.75rem 0;
  }
  
  .footer-inner {
    padding: 0 1.25rem;
  }
  
  .logo {
    height: 2rem;
  }
  
  .email {
    font-size: 0.95rem;
  }
}
</style>
