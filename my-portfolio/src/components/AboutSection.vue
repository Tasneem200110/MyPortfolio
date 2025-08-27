<template>
  <section id="about" class="about">
    <h2 class="section-title fade-up">
      <span class="strong">About Me</span>
    </h2>
    <div class="about-inner">
      <div class="left">
        <div class="image-frame">
          <img class="about-img" :src="imageSrc" :alt="imageAlt" />
        </div>
      </div>
      <div class="right">
        <p class="desc fade-up delay-1">
          Hi, I’m Tasneem Mostafa, a passionate Full Stack .NET Developer with a strong foundation in both backend development and frontend technologies. I graduated from the Faculty of Commerce, Management Information Systems (MIS), with a Very Good grade, and have completed several intensive training programs and internships that strengthened my technical expertise.</p>
        <p class="desc fade-up delay-2">
          I enjoy building scalable web applications using C#, ASP.NET Core, SQL Server, and Entity Framework, while also enhancing the user experience through HTML, CSS, JavaScript, and modern frameworks. My unique background in business and technology allows me to design solutions that are not only technically sound but also aligned with real-world needs.</p>
        <p class="desc fade-up delay-3">
          I’m always eager to learn, take on new challenges, and contribute to impactful projects. My goal is to grow as a developer and create digital solutions that make a difference.</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  imageSrc: {
    type: String,
    default: '../src/assets/IMG_5263.png'
  },
  imageAlt: { type: String, default: 'About illustration' }
})

const imageSrc = computed(() => props.imageSrc)
const imageAlt = computed(() => props.imageAlt)
</script>

<style scoped>
.about {
  background: #ffffff;
  padding: 4rem 0;
  overflow: hidden;
}

.about-inner {
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr;
  gap: 2.5rem;
  align-items: center;
  padding: 0 1rem;
}

.section-title {
  margin: 0 0 1.25rem 0;
  font-size: clamp(2rem, 5vw, 2.5rem);
  color: #0b0b0b;
  text-align: center;
}

.strong { 
  font-weight: 800; 
  color: #0b0b0b;
  background: #0b0b0b;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.desc {
  margin: 1rem 0 0 0;
  color: #4b4b4b;
  line-height: 1.7;
  font-size: clamp(1rem, 2vw, 1.125rem);
  text-align: left;
}

.left { 
  display: grid; 
  place-items: center;
  order: -1;
  justify-content: flex-start;
}
.image-frame {
  background: radial-gradient(120% 120% at 100% 0%, #e6f0ff 0%, #fde7ee 50%, #ffffff 100%);
  padding: 1.25rem;
  border-radius: 1.5rem;
  box-shadow: 0 12px 40px rgba(0,0,0,0.08);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.4s cubic-bezier(.2,.8,.2,1), box-shadow 0.4s ease;
  will-change: transform, box-shadow;
  animation: popIn 0.8s ease 0.2s both;
  width: 100%;
  max-width: 400px;
  margin: 0 auto;
}

.about-img {
  width: 100%;
  height: auto;
  object-fit: contain;
  border-radius: 1rem;
  will-change: transform;
  animation: floatY 6.4s ease-in-out 1s infinite;
  aspect-ratio: 1;
  object-position: center;
}

.image-frame:hover { 
  transform: translateY(-6px) rotate(-0.6deg); 
  box-shadow: 0 18px 52px rgba(0,0,0,0.14); 
}

/* Responsive Adjustments */
@media (min-width: 640px) {
  .about-inner {
    width: 85%;
    padding: 0 2rem;
  }
  
  .about-img {
    max-width: 400px;
  }
}

@media (min-width: 768px) {
  .about-inner {
    grid-template-columns: 1fr 1fr;
    gap: 3rem;
    align-items: center;
  }
  
  .left {
    order: 0;
  }
  
  .section-title {
    text-align: center;
    margin-bottom: 2rem;
  }
  
  .desc {
    font-size: 1.05rem;
  }
}

@media (min-width: 1024px) {
  .about {
    padding: 5rem 0;
  }
  
  .about-inner {
    width: 90%;
    max-width: 1200px;
    gap: 4rem;
  }
  
  .about-img {
    max-width: 100%;
  }
}

/* Animations */
.fade-up { opacity: 0; transform: translateY(14px); animation: fadeUp 0.8s ease forwards; }
.delay-1 { animation-delay: 0.12s; }
.delay-2 { animation-delay: 0.24s; }
.delay-3 { animation-delay: 0.36s; }

@keyframes fadeUp { from { opacity: 0; transform: translateY(14px); } to { opacity: 1; transform: translateY(0); } }
@keyframes popIn { 0% { opacity: 0; transform: translateY(16px) scale(.98); } 60% { opacity: 1; transform: translateY(0) scale(1.01); } 100% { opacity: 1; transform: translateY(0) scale(1); } }
@keyframes floatY { 0% { transform: translateY(0); } 50% { transform: translateY(-10px); } 100% { transform: translateY(0); } }

/* Accessibility: Reduced Motion */
@media (prefers-reduced-motion: reduce) {
  .fade-up, 
  .image-frame, 
  .about-img { 
    animation: none !important; 
    transform: none !important; 
    transition: none !important; 
  }
  
  .about-inner {
    gap: 2rem;
  }
}
</style>
