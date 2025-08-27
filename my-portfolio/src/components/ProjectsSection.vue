<template>
  <section id="projects" class="projects">
    <div class="projects-inner">
      <h2 class="section-title fade-up"><span class="strong">My Projects</span></h2>

      <ul class="list" role="list">
        <li v-for="(p, i) in items" :key="i" :class="['project-row', { alt: i % 2 === 1 }]">
          <div class="image-col">
            <div class="image-frame">
              <img class="project-img" :src="p.image" :alt="p.title" />
            </div>
          </div>

          <div class="content-col">
            <div class="index">{{ (i + 1).toString().padStart(2, '0') }}</div>
            <h3 class="title">{{ p.title }}</h3>
            <div class="meta">
              <span class="role" v-if="p.role">{{ p.role }}</span>
              <span class="date" v-if="p.date">• {{ p.date }}</span>
            </div>
            <p class="summary">{{ p.summary }}</p>
            <ul class="bullets">
              <li v-for="(b, bi) in p.points" :key="bi">{{ b }}</li>
            </ul>
            <div class="links" v-if="p.link">
              <a class="ext" :href="p.link" target="_blank" rel="noopener" aria-label="Open project">
                <i class="fa-solid fa-arrow-up-right-from-square"></i>
              </a>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  projects: {
    type: Array,
    default: () => ([
      {
        title: 'BoltFix – Smart Home Services Platform',
        role: 'Vue.js Developer',
        date: 'Jul 2025 – Aug 2025',
        summary: 'Smart home services platform with responsive booking, technician profiles, real-time updates, and secure auth.',
        points: [
          'Developed responsive front-end for booking workflows and technician profiles.',
          'Integrated secure authentication and improved performance on mobile and desktop.'
        ],
        image: '../src/assets/hero section.jpg',
        link: '#'
      },
      {
        title: 'AdventureNest – Camp & Entertainment Reservation System',
        role: 'ASP.NET MVC',
        date: 'Oct 2024',
        summary: 'Reservation system with event filtering, booking, and email confirmations.',
        points: [
          'Created with ASP.NET MVC including filtering, booking, and email confirmations.',
          'Built admin dashboard for events, reservations, and payments.'
        ],
        image: '../src/assets/hero section.jpg',
        link: '#'
      },
      {
        title: 'E-Commerce Platform',
        role: 'Full-Stack (ASP.NET Web API, SQL Server, Stripe)',
        date: 'Nov 2023',
        summary: 'Full-stack e-commerce with payments and optimized DB access.',
        points: [
          'Implemented payments with Stripe and secured APIs.',
          'Optimized SQL queries by ~30% for faster performance.'
        ],
        image: '../src/assets/hero section.jpg',
        link: '#'
      },
      {
        title: 'CRUD Management System',
        role: 'ASP.NET MVC',
        date: 'Oct 2023',
        summary: 'MVC-based CRUD app with validation and streamlined forms.',
        points: [
          'Added form validation and UX improvements, reducing data entry time by ~25%.'
        ],
        image: '../src/assets/hero section.jpg',
        link: '#'
      }
    ])
  }
})

const items = computed(() => props.projects)
</script>

<style scoped>
.projects {
  background: #0c0c0c;
  color: #eaeaea;
  padding: 80px 0;
}
.projects-inner { margin: 0 120px; }
.section-title { text-align: center; margin: 0 0 28px 0; font-size: clamp(28px, 5vw, 40px); }
.strong { font-weight: 800; }

.list {
  list-style: none;
  margin: 0;
  padding: 0;
  display: grid;
  gap: 56px;
}
.project-row {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 28px;
  align-items: center;
  opacity: 0;
  transform: translateY(18px);
  animation: fadeUp 0.8s ease forwards;
  border-bottom: 1px solid rgba(255,255,255,0.06);
  padding-bottom: 28px;
}
.project-row:nth-child(1) { animation-delay: 0.06s; }
.project-row:nth-child(2) { animation-delay: 0.14s; }
.project-row:nth-child(3) { animation-delay: 0.22s; }
.project-row:nth-child(4) { animation-delay: 0.30s; }

/* Alternate layout (image right, content left) */
.project-row.alt .image-col { order: 2; }
.project-row.alt .content-col { order: 1; }

.image-col { display: grid; }
.image-frame {
  background: #141414; border: 1px solid rgba(255,255,255,0.08); border-radius: 18px;
  padding: 10px; display: grid; place-items: center; box-shadow: 0 10px 26px rgba(0,0,0,0.25);
  transition: transform 0.35s cubic-bezier(.2,.8,.2,1), box-shadow 0.35s ease; will-change: transform, box-shadow;
  animation: popIn 0.8s ease 0.2s both;
}
.image-frame:hover { transform: translateY(-6px) rotate(-0.6deg); box-shadow: 0 16px 40px rgba(0,0,0,0.35); }
.project-img { width: 100%; height: auto; object-fit: cover; border-radius: 12px; display: block; }

.content-col { min-width: 0; }
.index { font-size: clamp(34px, 5vw, 56px); font-weight: 800; color: #b5b5b5; line-height: 1; }
.title { margin: 4px 0 8px 0; font-size: clamp(20px, 3.6vw, 28px); color: #ffffff; font-weight: 800; }
.meta { color: #cfcfcf; font-size: 14px; margin-bottom: 6px; }
.summary { color: #cfcfcf; margin: 8px 0 0 0; line-height: 1.7; }
.bullets { color: #bdbdbd; margin: 8px 0 0 18px; padding: 0; }
.bullets li { margin: 4px 0; }
.links { margin-top: 10px; }
.ext { display: inline-flex; align-items: center; justify-content: center; width: 36px; height: 36px; border-radius: 10px; border: 1px solid rgba(255,255,255,0.12); color: #fff; transition: transform 0.15s ease, background 0.2s ease, border-color 0.2s ease; backdrop-filter: blur(2px); }
.ext:hover { transform: translateY(-2px); background: #1c1c1c; border-color: rgba(255,255,255,0.24); }

/* Animations */
.fade-up { opacity: 0; transform: translateY(14px); animation: fadeUp 0.7s ease forwards; }
@keyframes fadeUp { from { opacity: 0; transform: translateY(14px); } to { opacity: 1; transform: translateY(0); } }
@keyframes popIn { 0% { opacity: 0; transform: translateY(16px) scale(.98); } 60% { opacity: 1; transform: translateY(0) scale(1.01); } 100% { opacity: 1; transform: translateY(0) scale(1); } }

@media (max-width: 900px) {
  .projects-inner { margin: 0 16px; }
  .project-row { grid-template-columns: 1fr; }
}

@media (prefers-reduced-motion: reduce) {
  .fade-up, .project-row, .image-frame { animation: none !important; transform: none !important; transition: none !important; }
}
</style>
