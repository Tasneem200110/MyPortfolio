<script setup>
import HeroSection from '@/components/HeroSection.vue'
import SkillsSection from '@/components/SkillsSection.vue'
import ExperienceSection from '@/components/ExperienceSection.vue'
import AboutSection from '@/components/AboutSection.vue'
import ProjectsSection from '@/components/ProjectsSection.vue'
import ContactSection from '@/components/ContactSection.vue'
import FooterSection from '@/components/FooterSection.vue'
import project1Img from '@/assets/hero section.jpg'
import project2Img from '@/assets/picture3.png'
import project3Img from '@/assets/picture2.png'
import project4Img from '@/assets/picture1.png'
import project5Img from '@/assets/picture5.png'
import heroImg from '@/assets/whatsapp.png'

</script>

<template>
  <HeroSection
    name="Tasneem Mostafa"
    location="Giza, Egypt"
    :links="{ github: 'https://github.com/Tasneem200110', linkedin: 'https://www.linkedin.com/in/tasneem-mostafa2001/', whatsapp: 'https://wa.me/01119360459' }"
    :image-src="heroImg"
    image-alt="Developer illustration"
  />

  
  <SkillsSection />

  
  
<ExperienceSection />
<AboutSection />
<ProjectsSection
  
    :projects="[
      {
        title: 'BoltFix – Smart Home Services Platform',
        role: 'Vue.js Developer',
        date: 'Jul 2025 – Aug 2025',
        summary: 'Developed responsive front‑end for booking workflows, technician profiles, and real-time updates. Integrated secure authentication and improved performance for mobile and desktop.',
        points: [
          'Responsive booking workflows and technician profiles',
          'Secure authentication and performance improvements'
        ],
        image: project1Img,
        link: 'https://iti-grad-project.vercel.app/'
      },
      {
        title: 'Tradex – Corporate Business Website',
        role: 'Frontend Developer',
        date: 'Jan-2025',
        summary: 'I developed a fully responsive multi-page corporate business website for Tradex, focusing on a clean and professional UI with modern web standards.',
        points: [
          'Multi-Page Layout: Includes Home, About, Headers, Blog, Services, Features, Pages, and Contact sections',
          'Responsive Design: Ensures website is accessible on all devices',
          'Modern UI: Clean and professional design with modern web standards',
          'Reusable Components: Navigation bar, footer, and styled sections implemented across all pages',
          'Implemented a dynamic product catalog with real-time updates and search functionality'
        ],
        image: project2Img,
        link: 'https://github.com/Tasneem200110/Tradex'
      },
      {
        title: 'RIVO – Fashion E-Commerce Website',
        role: 'Frontend Developer',
        date: 'Dec-2024',
        summary: 'I developed a modern, responsive Website for a fashion e-commerce brand using clean UI design principles and a fresh green-themed color palette.',
        points: [
          'Modern, responsive Website',
          'Clean UI design principles',
          'Reusable Components: Navigation bar, footer, and styled sections implemented across all pages.',
          'Implemented a dynamic product catalog with real-time updates and search functionality.'
        ],
        image: project3Img,
        link: 'https://github.com/Tasneem200110/Rivo-Frontend'
      },
      {
        title: 'AdventureNest – Camp & Entertainment Reservation System',
        role: 'ASP.NET MVC',
        date: 'Oct 2024',
        summary: 'Created with ASP.NET MVC, supporting event filtering, booking, and email confirmations. Built admin dashboard for events, reservations, and payments.',
        points: [
          'Event filtering, booking, and email confirmations',
          'Admin dashboard for events, reservations, and payments'
        ],
        image: project4Img,
        link: 'https://github.com/Tasneem200110/Camp-EntertainmentReservation'
      },
      {
        title: 'E‑Commerce Platform',
        role: 'ASP.NET Web API, SQL Server, Stripe',
        date: 'Nov 2023',
        summary: 'Full‑stack system with payments; optimized SQL queries by ~30% for faster performance.',
        points: [
          'Stripe payments and secure APIs',
          'SQL optimization ~30% faster'
        ],
        image: project5Img,
        link: 'https://github.com/Tasneem200110/E-Commerce'
      },
      
    ]"
  />
  <ContactSection
    email="tasneemmostafa200110@gmail.com"
    phone="(+20) 1119360459"
    :links="{ github: 'https://github.com/Tasneem200110', linkedin: 'https://www.linkedin.com/in/tasneem-mostafa2001/', whatsapp: 'https://wa.me/01119360459' }"
  />
  <FooterSection email="tasneemmostafa200110@gmail.com" />
</template>
