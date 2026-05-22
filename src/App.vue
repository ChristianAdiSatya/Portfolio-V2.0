<template>
  <!-- Beautiful Custom Cursor follow spring lag -->
  <CustomCursor />

  <!-- Beautiful Premium Preloader -->
  <Preloader @loaded="onLoaded" />

  <!-- Main Website Content Wrapper -->
  <div :class="{ 'opacity-0': !isLoaded }" class="transition-opacity duration-700 ease-in-out">
    <Hero ref="heroRef" />
    <About />
    <Skills />
    <Projects />
    <Footer />
    <Header />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Preloader from './components/Preloader.vue'
import Header from './components/header.vue'
import Hero from './page/hero.vue'
import About from './page/about.vue'
import Skills from './page/skills.vue'
import Footer from './components/footer.vue'
import Projects from './page/projects.vue'
import CustomCursor from './components/CustomCursor.vue'
import './components/card.vue'

const isLoaded = ref(false)
const heroRef = ref(null)

const onLoaded = () => {
  isLoaded.value = true
  document.body.style.overflow = ''
  
  // Trigger the premium entrance animations on the Hero component
  if (heroRef.value && typeof heroRef.value.playEntrance === 'function') {
    heroRef.value.playEntrance()
  }
}

onMounted(() => {
  // Prevent browser from automatically restoring scroll position on reload/load
  if ('scrollRestoration' in history) {
    history.scrollRestoration = 'manual'
  }
  window.scrollTo(0, 0)

  // Lock scrolling while the preloader screen is active
  document.body.style.overflow = 'hidden'
})
</script>

<style>
/* Disable native cursor on desktop to prioritize premium custom cursor experience */
@media (pointer: fine) {
  body, 
  a, 
  button, 
  [role="button"], 
  .project-card, 
  .skill-card, 
  input, 
  textarea, 
  select,
  .preloader-panel {
    cursor: none !important;
  }
}
</style>