<template>
  <section id="skills" class="skills">
    <div class="skills-inner">
      <h2 class="section-title fade-up">
        <span class="strong">My Skills</span>
      </h2>

      <div v-for="(g, gi) in groups" :key="gi" class="group-block fade-up" :style="{ animationDelay: (0.12 + gi * 0.08) + 's' }">
        <h3 class="sub-title">{{ g.title }}</h3>
        <ul class="grid stagger" role="list">
          <li v-for="(s, i) in g.items" :key="i" class="card" :class="s.variant">
            <div class="icon-wrap">
              <img v-if="s.source" :src="s.source" :alt="s.label" class="icon-img" />
              <i v-else :class="s.icon"></i>
            </div>
            <div class="label">{{ s.label }}</div>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  skills: {
    type: Array,
    default: () => ([
      // Programming Languages & Frameworks
      { icon: 'fa-solid fa-code', label: 'C#', variant: 'outline' },
      { icon: 'fa-brands fa-microsoft', label: 'ASP.NET Core', variant: 'outline' },
      { icon: 'fa-solid fa-database', label: 'Entity Framework', variant: 'outline' },
      { icon: 'fa-brands fa-js', label: 'JavaScript', variant: 'outline' },
      { icon: 'fa-brands fa-js', label: 'TypeScript', variant: 'outline' },
      { icon: 'fa-brands fa-angular', label: 'Angular', variant: 'outline' },
      { icon: 'fa-brands fa-vuejs', label: 'Vue.js', variant: 'outline' },

      // Backend & Database
      { icon: 'fa-solid fa-database', label: 'SQL Server', variant: 'outline' },
      { icon: 'fa-solid fa-cloud', label: 'RESTful APIs', variant: 'outline' },
      { icon: 'fa-solid fa-signal', label: 'SignalR', variant: 'outline' },

      // Frontend
      { icon: 'fa-brands fa-html5', label: 'HTML5', variant: 'outline' },
      { icon: 'fa-brands fa-css3', label: 'CSS3', variant: 'outline' },
      { icon: 'fa-brands fa-bootstrap', label: 'Bootstrap', variant: 'outline' },
      { icon: 'fa-solid fa-code', label: 'jQuery', variant: 'outline' },

      // Tools
      { icon: 'fa-brands fa-microsoft', label: 'Visual Studio', variant: 'outline' },
      { icon: 'fa-solid fa-code', label: 'VS Code', variant: 'outline' },
      { icon: 'fa-brands fa-git-alt', label: 'Git', variant: 'outline' },
      { icon: 'fa-brands fa-github', label: 'GitHub', variant: 'outline' },
      { icon: 'fa-solid fa-paper-plane', label: 'Postman', variant: 'outline' },
      { icon: 'fa-solid fa-book', label: 'Swagger', variant: 'outline' },
      { icon: 'fa-solid fa-database', label: 'SSMS', variant: 'outline' },

      // Concepts
      { icon: 'fa-solid fa-cubes', label: 'OOP', variant: 'outline' },
      { icon: 'fa-solid fa-code-branch', label: 'Data Structures', variant: 'outline' },
      { icon: 'fa-solid fa-list-check', label: 'Algorithms', variant: 'outline' },
      { icon: 'fa-solid fa-diagram-project', label: 'Design Patterns', variant: 'outline' },
      { icon: 'fa-solid fa-people-group', label: 'Agile/Scrum', variant: 'outline' },

      // Design & UI/UX
      { icon: 'fa-brands fa-figma', label: 'Figma', variant: 'outline' },
      { source: '../src/assets/photoshop.png', label: 'Adobe Photoshop', variant: 'outline' },
      { source: '../src/assets/illustrator.png', label: 'Adobe Illustrator', variant: 'outline' },
    ])
  }
})

const items = computed(() => props.skills)

const groups = computed(() => {
  const programming = ['C#','ASP.NET Core','Entity Framework','JavaScript','TypeScript','Angular','Vue.js']
  const backend = ['SQL Server','RESTful APIs','SignalR']
  const frontend = ['HTML5','CSS3','Bootstrap','jQuery']
  const tools = ['Visual Studio','VS Code','Git','GitHub','Postman','Swagger','SSMS']
  const concepts = ['OOP','Data Structures','Algorithms','Design Patterns','Agile/Scrum']
  const design = ['Figma','Adobe Photoshop','Adobe Illustrator']

  const by = (names) => items.value.filter(s => names.includes(s.label))
  return [
    { title: 'Programming Languages & Frameworks', items: by(programming) },
    { title: 'Backend & Database', items: by(backend) },
    { title: 'Frontend', items: by(frontend) },
    { title: 'Tools', items: by(tools) },
    { title: 'Concepts', items: by(concepts) },
    { title: 'Design & UI/UX', items: by(design) },
  ].filter(g => g.items.length)
})
</script>

<style scoped>
.skills {
  background: #fff;
  padding: 72px 0;
}
.skills-inner {
  margin: 0 120px;
}
.section-title {
  margin: 0 0 28px 0;
  text-align: center;
  font-size: clamp(28px, 5vw, 40px);
  color: #0b0b0b;
}
.strong { font-weight: 800; }

.group-block { margin-top: 26px; }
.sub-title {
  margin: 0 0 14px 0;
  text-align: center;
  font-size: clamp(18px, 3.2vw, 22px);
  color: #0b0b0b;
  font-weight: 700;
}

.grid {
  list-style: none;
  padding: 0;
  margin: 24px 0 0 0;
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  justify-content: center;
  gap: 18px;
}

/* Staggered reveal for cards */
.stagger .card {
  opacity: 0;
  transform: translateY(12px);
  animation: fadeUp 0.6s ease forwards;
}
/* Nth-child delays for smoother wave reveal */
.stagger .card:nth-child(1) { animation-delay: 0.02s; }
.stagger .card:nth-child(2) { animation-delay: 0.06s; }
.stagger .card:nth-child(3) { animation-delay: 0.10s; }
.stagger .card:nth-child(4) { animation-delay: 0.14s; }
.stagger .card:nth-child(5) { animation-delay: 0.18s; }
.stagger .card:nth-child(6) { animation-delay: 0.22s; }
.stagger .card:nth-child(7) { animation-delay: 0.26s; }
.stagger .card:nth-child(8) { animation-delay: 0.30s; }
.stagger .card:nth-child(9) { animation-delay: 0.34s; }
.stagger .card:nth-child(10) { animation-delay: 0.38s; }
.stagger .card:nth-child(11) { animation-delay: 0.42s; }
.stagger .card:nth-child(12) { animation-delay: 0.46s; }

.card {
  border: 1.5px solid #0b0b0b;
  border-radius: 12px;
  padding: 14px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  aspect-ratio: 1 / 1; /* make square */
  text-align: center;
  transition: transform 0.12s ease, box-shadow 0.2s ease, background 0.2s ease, color 0.2s ease;
  color: #0b0b0b;
}
.card.outline { background: #fff; }
.card.filled { /* kept for compatibility if used externally */
  background: #0b0b0b;
  color: #fff;
  border-color: transparent;
}
.card:hover {
  background: #0b0b0b;
  color: #fff;
  border-color: transparent;
  transform: translateY(-3px);
  box-shadow: 0 10px 28px rgba(0,0,0,0.12);
}

/* Fix nested selector for icon image on hover */
.card:hover .icon-img {
  transform: scale(1.1);
  background-color: #fff;
  border-radius: 14px;
}

/* Subtle press effect */
.card:active {
  transform: translateY(-1px);
}

.icon-wrap {
  font-size: 34px; /* fontawesome icon size */
  line-height: 1;
  width: 56px;
  height: 56px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
.icon-img {
  max-width: 42px;
  max-height: 42px;
  width: auto;
  height: auto;
  object-fit: contain;
  display: block;
  transition: transform 0.2s ease;
}

.label { margin-top: 10px; font-weight: 700; }

/* Entry utility for section/group titles (reuses from Hero) */
.fade-up {
  opacity: 0;
  transform: translateY(12px);
  animation: fadeUp 0.7s ease forwards;
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(12px); }
  to { opacity: 1; transform: translateY(0); }
}

/* Respect reduced motion */
@media (prefers-reduced-motion: reduce) {
  .fade-up,
  .stagger .card {
    animation: none !important;
    opacity: 1 !important;
    transform: none !important;
  }
}

@media (max-width: 1100px) {
  .grid { grid-template-columns: repeat(4, 1fr); }
}
@media (max-width: 800px) {
  .skills-inner { margin: 0 16px; }
  .grid { grid-template-columns: repeat(3, 1fr); }
}
@media (max-width: 520px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
}
</style>
