<template>
  <section id="experience" class="experience">
    <div class="experience-inner">
      <h2 class="section-title fade-up"><span class="strong">My Experience</span></h2>

      <ul class="cards stagger" role="list">
        <li v-for="(item, i) in items" :key="i" class="card">
          <div class="badge">
            <i :class="item.icon"></i>
          </div>
          <div class="content">
            <div class="header">
              <h3 class="role">{{ item.role }}</h3>
              <span class="date">{{ item.date }}</span>
            </div>
            <div class="org">{{ item.org }}</div>
            <p class="desc">{{ item.summary }}</p>
            <ul class="bullets">
              <li v-for="(b, bi) in item.points" :key="bi">{{ b }}</li>
            </ul>
          </div>
        </li>
      </ul>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  experiences: {
    type: Array,
    default: () => ([
      {
        icon: 'fa-solid fa-pen-ruler',
        role: 'UI/UX Developer (Trainee)',
        org: 'Intensive Training Program, Information Technology Institute (ITI) — Cairo Branch, Egypt',
        date: 'Mar 2025 – Aug 2025',
        summary: 'Participated in the Information Technology Institute’s intensive training program, focusing on user interface and user experience design. Gained hands-on experience in:',
        points: [
            'Built interactive UI components with Vue.js, Bootstrap, Tailwind CSS improving usability and accessibility.',
            'Creating responsive layouts using HTML, CSS, and JavaScript.',
            'Applied secure coding practices and modern UI/UX principles to ensure responsive, user-friendly designs.',
            'Designing and prototyping user-friendly, responsive web and mobile interfaces.',
            'Applying UI/UX principles, usability testing, and accessibility standards.',
            'Working with design tools (e.g., Figma, Adobe XD) to create interactive wireframes and high-fidelity prototypes.'
        ],
      },
      {
        icon: 'fa-solid fa-paintbrush',
        role: 'Web Designer (Intern)',
        org: 'NTI',
        date: 'Nov 2024 – Jan 2025',
        summary: 'Completed a professional internship focused on web design and development, where I:',
        points: [
          'Designed and built responsive web pages using HTML, CSS, and JavaScript.',
          'Gained practical experience in turning design concepts into functional web solutions.',
          'Applied UI/UX principles to create visually appealing and user-friendly layouts.',
          'Collaborated with team members to implement design requirements and improve usability.'
        ],
      },
      {
        icon: 'fa-solid fa-code',
        role: '.NET Developer (Intern)',
        org: 'DEPI',
        date: 'Apr 2024 – Oct 2024',
        summary: 'Delivered full-stack features and optimized APIs and backend performance.',
        points: [
            'Developed and maintained web applications using C#, ASP.NET Core, and MVC architecture.',
            'Worked with SQL Server to design, query, and manage databases.',
            'Collaborated in team projects, following Agile methodologies to deliver scalable applications.',
            'Applied OOP principles, Entity Framework, and LINQ to build efficient backend solutions.'
        ],
      },
      {
        icon: 'fa-solid fa-database',
        role: 'Backend .NET Developer (Intern)',
        org: 'Route Academy',
        date: 'May 2023 – Nov 2023',
        summary: 'Built and deployed backend services with CI/CD and database optimizations.',
        points: [
          'Built and optimized backend services using C#, ASP.NET Core, and Web API.',
          'Designed and managed SQL Server databases, ensuring data integrity and performance.',
          'Applied SOLID principles, dependency injection, and layered architecture to build scalable and maintainable solutions.',
          'Implemented SignalR for real-time communication, enhancing user experience.',
          'Gained practical experience in applying SOLID principles, dependency injection, and layered architecture.',
          'Implemented RESTful APIs and integrated them with front-end applications.'
        ],
      }
    ])
  }
})

const items = computed(() => props.experiences)
</script>

<style scoped>
.experience {
  background: #0c0c0c;
  color: #eaeaea;
  padding: 80px 0;
}
.experience-inner { margin: 0 120px; }
.section-title {
  margin: 0 0 28px 0;
  text-align: center;
  font-size: clamp(28px, 5vw, 40px);
}
.strong { font-weight: 800; }

.cards {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 18px;
}
.stagger .card {
  opacity: 0;
  transform: translateY(14px);
  animation: fadeUp 0.7s ease forwards;
}
.stagger .card:nth-child(1) { animation-delay: 0.04s; }
.stagger .card:nth-child(2) { animation-delay: 0.10s; }
.stagger .card:nth-child(3) { animation-delay: 0.16s; }
.stagger .card:nth-child(4) { animation-delay: 0.22s; }
.stagger .card:nth-child(5) { animation-delay: 0.28s; }
.stagger .card:nth-child(6) { animation-delay: 0.34s; }
.card {
  display: grid;
  grid-template-columns: auto 1fr;
  align-items: start;
  gap: 16px;
  background: #141414;
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 14px;
  padding: 20px;
  box-shadow: 0 10px 26px rgba(0,0,0,0.25);
  transition: transform 0.18s ease, box-shadow 0.25s ease, background 0.25s ease, border-color 0.25s ease;
}
.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 14px 36px rgba(0,0,0,0.35);
  border-color: rgba(255,255,255,0.14);
  background: #161616;
}
.badge {
  width: 40px;
  height: 40px;
  border-radius: 10px;
  display: grid;
  place-items: center;
  background: #202020;
  color: #fff;
  border: 1px solid rgba(255,255,255,0.08);
  transition: transform 0.18s ease, background 0.25s ease, border-color 0.25s ease;
}
.badge i { font-size: 18px; }
.card:hover .badge { transform: scale(1.06); background: #242424; border-color: rgba(255,255,255,0.16); }
.content { min-width: 0; }
.header {
  display: flex;
  justify-content: space-between;
  gap: 12px;
  align-items: baseline;
}
.role {
  margin: 0;
  font-size: 18px;
  font-weight: 800;
  color: #ffffff;
}
.date { color: #cfcfcf; font-size: 14px; white-space: nowrap; }
.org { color: #d7d7d7; font-weight: 600; margin-top: 2px; }
.desc { color: #bdbdbd; margin: 8px 0 0 0; }
.bullets { color: #bdbdbd; margin: 8px 0 0 18px; padding: 0; }
.bullets li { margin: 4px 0; }

/* Fade-up utility (consistent with other sections) */
.fade-up { opacity: 0; transform: translateY(14px); animation: fadeUp 0.7s ease forwards; }
@keyframes fadeUp { from { opacity: 0; transform: translateY(14px); } to { opacity: 1; transform: translateY(0); } }

/* Reduced motion */
@media (prefers-reduced-motion: reduce) {
  .fade-up,
  .stagger .card {
    animation: none !important;
    opacity: 1 !important;
    transform: none !important;
  }
}

@media (max-width: 900px) {
  .experience-inner { margin: 0 16px; }
  .header { flex-direction: column; gap: 4px; align-items: flex-start; }
}
</style>
