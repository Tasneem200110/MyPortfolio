<template>
  <section class="hero">
    <div class="hero-container">
      <div class="left">
        <h1 class="title fade-up">
          <span >Hello I’am </span>
          <span class="strong">{{ name }}.</span>
        </h1>
        <h2 class="subtitle fade-up delay-1">
          <span class="outlined">Full Stack .Net Developer</span>
        </h2>
        <h2 class="subtitle fade-up delay-2">
          <span>Based In </span>
          <span class="strong"> {{ location }}.</span>
        </h2>

        <p class="desc fade-up delay-3">
           {{ blurb }}
        </p>

        <div class="socials fade-up delay-4" aria-label="Social links">
          <a class="social outline" :href="links.github" target="_blank" aria-label="GitHub">
            <i class="fa-brands fa-github"></i>
          </a>
          <a class="social outline" :href="links.linkedin" target="_blank" aria-label="Linkedin">
            <i class="fa-brands fa-linkedin"></i>
          </a>
          <a class="social outline" :href="links.whatsapp" target="_blank" aria-label="Whatsapp">
            <i class="fa-brands fa-whatsapp"></i>
          </a>
        </div>
      </div>

      <div class="right">
        <div class="image-frame">
          <img class="hero-img" :src="imageSrc" :alt="imageAlt" />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'
import heroImg from '@/assets/hero section.jpg'

const props = defineProps({
  name: { type: String, default: 'Tasneem Mostafa' },
  location: { type: String, default: 'Giza, Egypt' },
  blurb: { type: String, default: `I’m Tasneem Mostafa, a passionate Full Stack .NET Developer with a strong background in C#, ASP.NET, SQL Server, and front-end frameworks. I enjoy building scalable, user-friendly applications and continuously enhancing my skills in backend and frontend development. With a business background in MIS, I bring a unique perspective that bridges technical solutions with real-world needs.` },
  imageSrc: { type: String, default: heroImg },
  imageAlt: { type: String, default: 'Hero illustration' },
  links: {
    type: Object,
    default: () => ({
      github: '#',
      linkedin: '#',
      whatsapp: '#',
    })
  }
})

const name = computed(() => props.name)
const location = computed(() => props.location)
const blurb = computed(() => props.blurb)
const imageSrc = computed(() => props.imageSrc)
const imageAlt = computed(() => props.imageAlt)
const links = computed(() => props.links)
</script>

<style scoped>

.hero {
  background: linear-gradient(135deg, #ffffff 0%, #f8e9ec 40%, #f0f4ff 100%);
  padding: 40px 0 !important;
  display: flex;
  align-items: center; 
  justify-content: space-between;

}

.hero-container {
  width: 100%;
  margin: 0 !important;
  padding: 0 120px;
  display: grid;
  gap: 30px !important;
  grid-template-columns: 1fr;
  align-items: center;
  box-sizing: border-box;
}

/* Mobile styles */
@media (max-width: 1023px) {

  .socials {
    justify-content: center;
  }
}

.left {
  order: 2;
  text-align: center;
}

.right {
  order: 1;
  display: flex;
  justify-content: flex-end;
  margin-bottom: 32px;
}

.title {
  margin: 0 0 12px 0;
  font-size: clamp(32px, 7vw, 52px);
  line-height: 1.15;
  color: #0b0b0b;
  font-weight: 800;
}

.subtitle {
  margin: 0 0 12px 0;
  font-size: clamp(24px, 5vw, 40px);
  line-height: 1.2;
  color: #0b0b0b;
  font-weight: 700;
}

.muted { 
  color: #4b4b4b; 
  font-weight: 500; 
}

.strong { 
  font-weight: 800; 
  color: #0b0b0b;
  position: relative;
  display: inline-block;
}

.strong::after {
  content: '';
  position: absolute;
  bottom: 2px;
  left: 0;
  width: 100%;
  height: 8px;
  background: linear-gradient(90deg, rgba(11,11,11,0.15) 0%, rgba(11,11,11,0) 100%);
  z-index: -1;
  border-radius: 4px;
}

.outlined {
  font-weight: 900;
  color: transparent;
  -webkit-text-stroke: 2px #111;
}

.desc {
  margin: 24px auto 0;
  max-width: 56ch;
  color: #5b5b5b;
  line-height: 1.7;
  font-size: 16px;
  font-weight: 400;
  letter-spacing: 0.01em;
  text-align: center;
}

.socials {
  display: flex;
  gap: 14px;
  margin-top: 26px;
}

.social {
  width: 44px;
  height: 44px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 10px;
  font-size: 16px;
  transition: transform 0.12s ease, background 0.2s ease, color 0.2s ease, box-shadow 0.2s ease;
}

.social.filled {
  background: #0b0b0b;
  color: #fff;
  box-shadow: 0 8px 24px rgba(0,0,0,0.12);
}

.social.outline {
  color: #0b0b0b;
  border: 1.5px solid #0b0b0b;
}

.social:hover { transform: translateY(-2px); }

.social:active { transform: translateY(0); }

/* Hover styles for social links */
.social.outline:hover {
  background: #0b0b0b;
  color: #ffffff;
  border-color: transparent;
  box-shadow: 0 10px 28px rgba(0,0,0,0.14);
}

.social.filled:hover {
  background: #111111;
  box-shadow: 0 12px 32px rgba(0,0,0,0.16);
}

.right { display: grid; place-items: center; }


.hero-img {
  width: 100%;
  height: auto;
  max-width: 400px;
  object-fit: contain;
  border-radius: 16px;
  will-change: transform;
  animation: floatY 6s ease-in-out 1.2s infinite;
  box-shadow: 0 20px 40px rgba(0,0,0,0.1);
}


/* Responsive adjustments */
@media (min-width: 768px) {
  .hero {
    padding: 100px 0 20px;
  }
  
  .hero-container {
    grid-template-columns: 1.1fr 0.9fr;
    gap: 60px;
    align-items: center;
    margin: 0 20px ;
  }
  
  .left {
    order: 1;
    text-align: left;
  }
  
  .right {
    order: 2;
    margin-bottom: 0;
  }
  
  .desc {
    text-align: left;
    margin: 24px 0 0 0;
  }
  
  .socials {
    justify-content: flex-start;
  }
  
  .image-frame {
    max-width: 520px;
  }
}



/* Animations */
.fade-up {
  opacity: 0;
  transform: translateY(20px);
  animation: fadeUp 0.8s ease forwards;
}

.delay-1 { animation-delay: 0.2s; }
.delay-2 { animation-delay: 0.3s; }
.delay-3 { animation-delay: 0.4s; }
.delay-4 { animation-delay: 0.5s; }

@keyframes fadeUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes popIn {
  0% {
    opacity: 0;
    transform: perspective(1000px) rotateY(-8deg) rotateX(4deg) scale(0.8) translateY(20px);
  }
  100% {
    opacity: 1;
    transform: perspective(1000px) rotateY(-8deg) rotateX(4deg) scale(1) translateY(0);
  }
}

@keyframes floatY {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

/* Respect users who prefer reduced motion */
@media (prefers-reduced-motion: reduce) {
  .fade-up,
  .image-frame,
  .hero-img {
    animation: none !important;
    transform: none !important;
    transition: none !important;
  }
}

@media (max-width: 920px) {
  .hero::after { right: -200px; top: -140px; width: 420px; height: 420px; }
  .container { grid-template-columns: 1fr; text-align: left; }
  .right { order: -1; }
  .hero { padding-top: 32px; }
}
</style>
