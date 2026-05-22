<template>
  <section id="skills" class="max-w-full mx-auto min-h-screen py-30 px-6 lg:px-14 bg-white border-b line-border overflow-hidden">
    <div class="max-w-full mx-auto">
      <!-- Title -->
      <span class="text-[12px] uppercase tracking-[0.5em] text-studio-muted mb-16 block text-right skills-reveal">
        - My Skills -
      </span>
      
      <!-- Asymmetric Bento Grid Layout -->
      <div class="grid grid-cols-1 md:grid-cols-12 gap-6 lg:gap-8">
        
        <!-- CARD 1: Web Development (Col-span 7) - Elegant white container with left-right split -->
        <div class="md:col-span-7 group bg-white border border-neutral-200/60 rounded-md overflow-hidden shadow-xs hover:shadow-lg transition-all duration-500 flex flex-col md:flex-row h-full bento-card">
          <!-- Text details -->
          <div class="p-8 flex flex-col justify-between flex-1">
            <div>
              <div class="flex items-center gap-2 mb-3">
                <span class="w-1.5 h-1.5 rounded-full bg-black"></span>
                <span class="text-[10px] tracking-widest font-mono text-gray-400 uppercase font-medium">Core Skill</span>
              </div>
              <h3 class="text-2xl font-normal tracking-wide uppercase text-neutral-800 mb-4 group-hover:text-black transition-colors duration-300">
                Web Developer
              </h3>
              <p class="text-gray-500 text-sm font-light leading-relaxed tracking-wide mb-6">
                Designing and engineering highly responsive, aesthetic, and highly functional websites using modern frontend frameworks and standard coding practices.
              </p>
            </div>
            
            <!-- Progress Bar -->
            <div class="mb-6">
              <div class="flex justify-between items-baseline mb-2 font-mono text-[10px]">
                <span class="text-gray-400 uppercase tracking-widest">Expertise Level</span>
                <span class="text-neutral-800 font-semibold text-xs">90%</span>
              </div>
              <div class="w-full h-[2px] bg-neutral-100 rounded-full overflow-hidden">
                <div class="h-full bg-black progress-fill" style="width: 0%" data-target="90%"></div>
              </div>
            </div>

            <!-- Tech Badges -->
            <div class="flex flex-wrap gap-1.5 pt-4 border-t border-neutral-100">
              <span v-for="tag in ['Vue.js', 'GSAP', 'Vite', 'Tailwind', 'JavaScript', 'HTML5/CSS3', 'PHP', 'Node.js', 'MySQL']" :key="tag" class="font-mono text-gray-500 tracking-wider text-[9px] bg-neutral-50 px-2.5 py-1 rounded-xs border border-neutral-200 uppercase font-light">
                {{ tag }}
              </span>
            </div>
          </div>

          <!-- Image block -->
          <div class="relative overflow-hidden w-full md:w-2/5 min-h-[220px] md:min-h-full aspect-[4/3] md:aspect-auto border-t md:border-t-0 md:border-l border-neutral-100">
            <img :src="imgCode" alt="Web Development" class="absolute inset-0 w-full h-full object-cover grayscale transition-all duration-750 ease-out group-hover:scale-105 group-hover:grayscale-0" />
          </div>
        </div>

        <!-- CARD 2: CCTV Systems (Col-span 5) - Full image background with cinematic overlay -->
        <div class="md:col-span-5 group relative rounded-md overflow-hidden shadow-xs hover:shadow-lg transition-all duration-500 min-h-[380px] flex flex-col justify-end p-8 text-white bento-card">
          <!-- Background image -->
          <img :src="imgCctv" alt="CCTV Systems" class="absolute inset-0 w-full h-full object-cover transition-transform duration-750 ease-out group-hover:scale-105" />
          <!-- Dark cinematic overlay -->
          <div class="absolute inset-0 bg-gradient-to-t from-black/95 via-black/60 to-black/35 group-hover:via-black/50 transition-all duration-500"></div>

          <!-- Content overlay -->
          <div class="relative z-10 flex flex-col justify-between h-full">
            <div class="flex justify-between items-start">
              <div class="flex items-center gap-2">
                <span class="w-1.5 h-1.5 rounded-full bg-white animate-pulse"></span>
                <span class="text-[10px] tracking-widest font-mono text-white/60 uppercase font-medium">Expertise</span>
              </div>
              <div class="text-[10px] font-mono tracking-widest text-white/50">SYSTEMS</div>
            </div>

            <div class="mt-auto">
              <h3 class="text-2xl font-normal tracking-wide uppercase mb-3">
                CCTV Technician
              </h3>
              <p class="text-white/70 text-sm font-light leading-relaxed tracking-wide mb-6">
                Professional layout planning, camera focus optimizations, custom PoE structured cabling, and central NVR configuration for industrial scale security.
              </p>

              <!-- Progress bar -->
              <div class="mb-6">
                <div class="flex justify-between items-baseline mb-2 font-mono text-[10px]">
                  <span class="text-white/50 uppercase tracking-widest">Expertise Level</span>
                  <span class="text-white font-semibold text-xs">95%</span>
                </div>
                <div class="w-full h-[2px] bg-white/20 rounded-full overflow-hidden">
                  <div class="h-full bg-white progress-fill" style="width: 0%" data-target="95%"></div>
                </div>
              </div>

              <!-- Tech tags -->
              <div class="flex flex-wrap gap-1.5 pt-4 border-t border-white/15">
                <span v-for="tag in ['PoE Systems', 'NVR/DVR', 'Structured Cabling', 'IP Routing', 'Alignment']" :key="tag" class="font-mono text-white/70 tracking-wider text-[9px] bg-white/10 px-2.5 py-1 rounded-xs border border-white/15 uppercase font-light">
                  {{ tag }}
                </span>
              </div>
            </div>
          </div>
        </div>

        <!-- CARD 3: IT Support (Col-span 5) - Full image background with cinematic overlay -->
        <div class="md:col-span-5 group relative rounded-md overflow-hidden shadow-xs hover:shadow-lg transition-all duration-500 min-h-[380px] flex flex-col justify-end p-8 text-white bento-card">
          <!-- Background image -->
          <img :src="imgItSupport" alt="IT Support" class="absolute inset-0 w-full h-full object-cover transition-transform duration-750 ease-out group-hover:scale-105" />
          <!-- Dark cinematic overlay -->
          <div class="absolute inset-0 bg-gradient-to-t from-black/95 via-black/60 to-black/35 group-hover:via-black/50 transition-all duration-500"></div>

          <!-- Content overlay -->
          <div class="relative z-10 flex flex-col justify-between h-full">
            <div class="flex justify-between items-start">
              <div class="flex items-center gap-2">
                <span class="w-1.5 h-1.5 rounded-full bg-white animate-pulse"></span>
                <span class="text-[10px] tracking-widest font-mono text-white/60 uppercase font-medium">Expertise</span>
              </div>
              <div class="text-[10px] font-mono tracking-widest text-white/50">MAINTENANCE</div>
            </div>

            <div class="mt-auto">
              <h3 class="text-2xl font-normal tracking-wide uppercase mb-3">
                IT Support
              </h3>
              <p class="text-white/70 text-sm font-light leading-relaxed tracking-wide mb-6">
                Diagnosing intricate hardware conflicts, network infrastructure security management, local server setups, and providing rapid on-site troubleshooting.
              </p>

              <!-- Progress bar -->
              <div class="mb-6">
                <div class="flex justify-between items-baseline mb-2 font-mono text-[10px]">
                  <span class="text-white/50 uppercase tracking-widest">Expertise Level</span>
                  <span class="text-white font-semibold text-xs">92%</span>
                </div>
                <div class="w-full h-[2px] bg-white/20 rounded-full overflow-hidden">
                  <div class="h-full bg-white progress-fill" style="width: 0%" data-target="92%"></div>
                </div>
              </div>

              <!-- Tech tags -->
              <div class="flex flex-wrap gap-1.5 pt-4 border-t border-white/15">
                <span v-for="tag in ['Diagnostics', 'Server Admin', 'Network Security', 'Active Directory', 'Troubleshoot']" :key="tag" class="font-mono text-white/70 tracking-wider text-[9px] bg-white/10 px-2.5 py-1 rounded-xs border border-white/15 uppercase font-light">
                  {{ tag }}
                </span>
              </div>
            </div>
          </div>
        </div>

        <!-- CARD 4: Phone Repair (Col-span 7) - Elegant white container with left-right split -->
        <div class="md:col-span-7 group bg-white border border-neutral-200/60 rounded-md overflow-hidden shadow-xs hover:shadow-lg transition-all duration-500 flex flex-col md:flex-row h-full bento-card">
          <!-- Image block -->
          <div class="relative overflow-hidden w-full md:w-2/5 min-h-[220px] md:min-h-full aspect-[4/3] md:aspect-auto border-b md:border-b-0 md:border-r border-neutral-100">
            <img :src="imgPhoneRepair" alt="Phone Repair" class="absolute inset-0 w-full h-full object-cover grayscale transition-all duration-750 ease-out group-hover:scale-105 group-hover:grayscale-0" />
          </div>
          
          <!-- Text details -->
          <div class="p-8 flex flex-col justify-between flex-1">
            <div>
              <div class="flex items-center gap-2 mb-3">
                <span class="w-1.5 h-1.5 rounded-full bg-black"></span>
                <span class="text-[10px] tracking-widest font-mono text-gray-400 uppercase font-medium">Core Skill</span>
              </div>
              <h3 class="text-2xl font-normal tracking-wide uppercase text-neutral-800 mb-4 group-hover:text-black transition-colors duration-300">
                Phone Repair
              </h3>
              <p class="text-gray-500 text-sm font-light leading-relaxed tracking-wide mb-6">
                Specialized micro-hardware repairs for modern flagship mobile devices, including OLED replacement, logic board diagnostics, and liquid damage recovery.
              </p>
            </div>
            
            <!-- Progress Bar -->
            <div class="mb-6">
              <div class="flex justify-between items-baseline mb-2 font-mono text-[10px]">
                <span class="text-gray-400 uppercase tracking-widest">Expertise Level</span>
                <span class="text-neutral-800 font-semibold text-xs">88%</span>
              </div>
              <div class="w-full h-[2px] bg-neutral-100 rounded-full overflow-hidden">
                <div class="h-full bg-black progress-fill" style="width: 0%" data-target="88%"></div>
              </div>
            </div>

            <!-- Tech Badges -->
            <div class="flex flex-wrap gap-1.5 pt-4 border-t border-neutral-100">
              <span v-for="tag in ['Micro-Soldering', 'OLED Assembly', 'Battery swaps', 'IP68 Sealing', 'Board Diagnostics']" :key="tag" class="font-mono text-gray-500 tracking-wider text-[9px] bg-neutral-50 px-2.5 py-1 rounded-xs border border-neutral-200 uppercase font-light">
                {{ tag }}
              </span>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import imgCode from '@/assets/code.jpg'
import imgCctv from '@/assets/cctv.jpg'
import imgItSupport from '@/assets/it-support.jpg'
import imgPhoneRepair from '@/assets/phone-repair.jpg'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  // Animate the "- My Skills -" header
  gsap.fromTo('.skills-reveal', 
    { y: 20, opacity: 0 },
    {
      y: 0,
      opacity: 1,
      duration: 1,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '#skills',
        start: 'top 50%',
        toggleActions: 'play none none none'
      }
    }
  )

  // Stagger entry for Bento Grid cards (left/right sliding door effect) + dynamic progress bars
  const cards = gsap.utils.toArray('.bento-card')
  const isMobileOrTablet = window.innerWidth < 1024
  const slideDistance = isMobileOrTablet ? 35 : 80

  cards.forEach((card, index) => {
    // If index is even (0, 2) it slides from left; if odd (1, 3) it slides from right
    const isLeft = index % 2 === 0
    const startX = isLeft ? -slideDistance : slideDistance

    gsap.fromTo(card, 
      { x: startX, opacity: 0 },
      {
        x: 0,
        opacity: 1,
        duration: 1.4,
        ease: 'power3.out',
        scrollTrigger: {
          trigger: card,
          start: 'top 50%',
          toggleActions: 'play none none none'
        }
      }
    )

    // Dynamic horizontal progress bar fill animation
    const fill = card.querySelector('.progress-fill')
    if (fill) {
      const targetWidth = fill.getAttribute('data-target')
      gsap.fromTo(fill,
        { width: '0%' },
        {
          width: targetWidth,
          duration: 1.5,
          ease: 'power2.out',
          delay: 0.2,
          scrollTrigger: {
            trigger: card,
            start: 'top 50%',
            toggleActions: 'play none none none'
          }
        }
      )
    }
  })
})
</script>

<style scoped>
/* Pre-hide elements to prevent sudden FOUC pops or flashes before ScrollTrigger fires */
.skills-reveal,
.bento-card {
  opacity: 0;
  will-change: transform, opacity;
}
</style>