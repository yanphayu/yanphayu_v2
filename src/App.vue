<script setup>
import { onMounted, onBeforeUnmount, nextTick } from 'vue'
import { activeSection } from './state.js'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import EducationSection from './components/EducationSection.vue'
import MusicSection from './components/MusicSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterBar from './components/FooterBar.vue'

let spyObserver = null

onMounted(async () => {
  await nextTick()

  /* ---------- Dock scroll-spy ---------- */
  const sections = Array.from(document.querySelectorAll('main section[id]'))
  if (sections.length && 'IntersectionObserver' in window) {
    spyObserver = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) activeSection.value = entry.target.id
        })
      },
      { rootMargin: '-45% 0px -50% 0px', threshold: 0 }
    )
    sections.forEach((sec) => spyObserver.observe(sec))
  }
})

onBeforeUnmount(() => {
  if (spyObserver) spyObserver.disconnect()
})
</script>

<template>
  <NavBar />
  <main>
    <HeroSection />
    <AboutSection />
    <SkillsSection />
    <ProjectsSection />
    <EducationSection />
    <MusicSection />
    <ContactSection />
  </main>
  <FooterBar />
</template>
