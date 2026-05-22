<template>
    <!-- Hero Section -->
    <section id="home" class="min-h-screen flex flex-col justify-end px-6 pb-12 border-b line-border">
        <div class="mb-12">
            <h1 class="text-huge font-semibold tracking-wide uppercase flex flex-col">
                <span class="overflow-hidden block leading-[1.05]">
                    <span class="hero-title-line inline-block">Hi! it's</span>
                </span>
                <span class="overflow-hidden block leading-[1.05]">
                    <span class="hero-title-line inline-block ml-[5vw]">Christian Adi</span>
                </span>
                <span class="overflow-hidden block leading-[1.05] hidden 2xl:block">
                    <span class="hero-title-line inline-block xl:ml-[10vw]">Satya.</span>
                </span>
            </h1>
        </div>
        <div class="flex flex-col md:flex-row justify-between items-end gap-6 overflow-hidden">
            <div class="max-w-xs text-sm uppercase tracking-widest leading-relaxed font-normal hero-fade-up opacity-0">
                <p class="text-gray-500">
                    Web Developer
                </p>
                <p class="text-gray-500">
                    CCTV Technician
                </p>
                <p class="text-gray-500">
                    IT Support
                </p>
            </div>
            <div class="text-sm uppercase tracking-[0.2em] font-normal hero-fade-up opacity-0">
                Scroll to explore ↓
            </div>
        </div>
    </section>
</template>

<script setup>
import { onMounted } from 'vue'
import gsap from 'gsap'

// Function to trigger the entrance stagger animations when preloader completes
const playEntrance = () => {
  const tl = gsap.timeline()
  
  // 1. Premium slide up for the huge split title text lines
  tl.fromTo('.hero-title-line', 
    { y: '100%', opacity: 0 },
    { y: '0%', opacity: 1, duration: 1.4, ease: 'power4.out', stagger: 0.18 }
  )
  
  // 2. Smooth fade and slide up for subtexts and scroll indicator
  tl.fromTo('.hero-fade-up', 
    { y: 35, opacity: 0 },
    { y: 0, opacity: 1, duration: 1.1, ease: 'power3.out', stagger: 0.12 },
    '-=0.9'
  )
  
  // 3. Smooth fade & slide down for the global navbar
  tl.fromTo('#navbar', 
    { y: -30, opacity: 0 },
    { y: 0, opacity: 1, duration: 1.0, ease: 'power3.out' },
    '-=1.0'
  )
}

onMounted(() => {
  // Set initial states for elements to prevent FOUC (flash of unstyled content)
  gsap.set('.hero-title-line', { y: '100%', opacity: 0 })
  gsap.set('.hero-fade-up', { y: 35, opacity: 0 })
  gsap.set('#navbar', { y: -30, opacity: 0 })
})

// Expose the method so that App.vue can trigger it at the exact moment the preloader finishes
defineExpose({
  playEntrance
})
</script>