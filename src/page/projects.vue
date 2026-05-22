<template>
  <section id="projects" class="max-w-full mx-auto min-h-screen py-30 px-6 lg:px-14 border-b line-border">
    <div class="max-w-full mx-auto">
      <!-- Title -->
      <span class="text-[12px] uppercase tracking-[0.5em] text-studio-muted mb-12 block">
        - Projects -
      </span>
      
      <!-- Premium Category Filters -->
      <div class="flex flex-wrap gap-3 mb-16 uppercase text-[10px] tracking-widest font-mono">
        <button 
          v-for="cat in categories" 
          :key="cat.value"
          @click="activeCategory = cat.value"
          :class="[
            'px-6 py-2.5 rounded-full border transition-all duration-300 cursor-pointer font-medium select-none',
            activeCategory === cat.value 
              ? 'bg-black border-black text-white' 
              : 'bg-transparent border-neutral-200 text-gray-500 hover:border-black hover:text-black'
          ]"
        >
          {{ cat.name }}
        </button>
      </div>

      <!-- Projects Grid using Vue TransitionGroup for fluid animating filters -->
      <div class="relative">
        <TransitionGroup 
          name="project-grid" 
          tag="div" 
          class="grid md:grid-cols-2 xl:grid-cols-3 gap-8 md:gap-10"
        >
          <div 
            v-for="project in filteredProjects" 
            :key="project.title" 
            class="project-card group bg-white border border-neutral-200/60 rounded-md overflow-hidden shadow-xs hover:shadow-lg transition-all duration-500 flex flex-col h-full"
          >
            <!-- Image Box with modern hover scale and floating badges -->
            <div class="relative overflow-hidden aspect-[4/3] bg-neutral-100">
              <img 
                :src="project.image" 
                :alt="project.title" 
                class="w-full h-full object-cover transition-transform duration-750 ease-out group-hover:scale-105" 
              />
              <!-- Year Floating Badge -->
              <div class="absolute top-4 right-4 bg-black/85 backdrop-blur-md text-white font-mono text-[9px] tracking-widest px-3 py-1 rounded-sm uppercase font-light">
                {{ project.year }}
              </div>
              <!-- Category Tag Overlay -->
              <div class="absolute bottom-4 left-4 bg-white/95 backdrop-blur-md text-black font-mono text-[9px] tracking-widest px-3 py-1 rounded-sm uppercase font-semibold">
                {{ project.category }}
              </div>
            </div>

            <!-- Project Metadata Card -->
            <div class="p-6 md:p-8 flex flex-col flex-grow justify-between">
              <div>
                <h3 class="text-xl font-normal tracking-wide uppercase text-neutral-800 mb-4 transition-colors duration-300 group-hover:text-black flex flex-col">
                  {{ project.title }}
                  <!-- Underline animation accent -->
                  <span class="h-[1px] bg-black w-0 group-hover:w-16 transition-all duration-500 mt-1.5"></span>
                </h3>
                <p class="text-gray-500 text-sm font-light leading-relaxed tracking-wide mb-6">
                  {{ project.description }}
                </p>
              </div>

              <!-- Conditional Tag Display for Website vs Other Categories -->
              <div v-if="project.category === 'WEBSITE'" class="space-y-4 pt-4 border-t border-neutral-100">
                <!-- Tech Stack Title and Tags -->
                <div>
                  <div class="text-[9px] font-mono tracking-[0.25em] uppercase text-neutral-400 mb-2 font-semibold">
                    Tech Stack
                  </div>
                  <div class="flex flex-wrap gap-1.5">
                    <span 
                      v-for="tag in project.tags" 
                      :key="tag" 
                      class="font-mono text-gray-500 tracking-wider text-[9px] bg-neutral-50 px-2 py-0.5 rounded-xs border border-neutral-200 uppercase font-light"
                    >
                      {{ tag }}
                    </span>
                  </div>
                </div>

                <!-- Features Title and Tags -->
                <div>
                  <div class="text-[9px] font-mono tracking-[0.25em] uppercase text-neutral-400 mb-2 font-semibold">
                    Key Features
                  </div>
                  <div class="flex flex-wrap gap-1.5">
                    <span 
                      v-for="feature in project.features" 
                      :key="feature" 
                      class="font-mono text-gray-500 tracking-wider text-[9px] bg-neutral-50 px-2 py-0.5 rounded-xs border border-neutral-200 uppercase font-light animate-pulse-subtle"
                    >
                      {{ feature }}
                    </span>
                  </div>
                </div>
              </div>

              <!-- Other Categories (Default Look) -->
              <div v-else class="flex flex-wrap gap-2 pt-4 border-t border-neutral-100">
                <span 
                  v-for="tag in project.tags" 
                  :key="tag" 
                  class="font-mono text-gray-500 tracking-wider text-[10px] bg-neutral-50 px-2.5 py-1 rounded-xs border border-neutral-200"
                >
                  {{ tag }}
                </span>
              </div>
            </div>
          </div>
        </TransitionGroup>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import poe from '@/assets/poe-installation.jpeg'
import server from '@/assets/cctv-server-installation.jpeg'
import battery from '@/assets/battery-repair.jpeg'
import camera from '@/assets/cctv-camera.jpeg'
import lcd from '@/assets/lcd-repair.jpeg'
import dvr from '@/assets/dvr-upgrade-hdd.jpeg'

// Web Projects Screenshots
import coletta from '@/assets/web-project/coletta.png'
import kapika from '@/assets/web-project/kapikawoodfest.png'
import lambang from '@/assets/web-project/lambangrattan.png'
import myservice from '@/assets/web-project/my-services.png'
import erp from '@/assets/web-project/MyService-Enterprise.png'

const activeCategory = ref('ALL')

const categories = [
  { name: 'Show All', value: 'ALL' },
  { name: 'Websites', value: 'WEBSITE' },
  { name: 'CCTV Systems', value: 'CCTV' },
  { name: 'Hardware Repairs', value: 'REPAIR' }
]

const projects = [
  {
    title: 'MyService Enterprise Dashboard',
    description: 'Developed an advanced web-based Enterprise Resource Planning (ERP) dashboard featuring real-time inventory levels, dynamic role-based access control, and technician dispatch systems.',
    image: erp,
    year: '2026',
    category: 'WEBSITE',
    tags: ['Vue.js', 'Tailwind CSS', 'MySQL', 'PHP', 'JavaScript'],
    features: ['Login Automation (With Role)', 'Integrated Invoice System'],
  },
  {
    title: 'Coletta Interior Landing Page',
    description: 'Designed and engineered an elegant, minimal architectural and interior design portfolio showcase website with premium aesthetics, fluid typography, and smooth layouts.',
    image: coletta,
    year: '2024',
    category: 'WEBSITE',
    tags: ['HTML5 CSS Vanilla', 'JavaScript', 'Minimal Design', 'GSAP'],
    features: ['Integrated Database'],
  },
  {
    title: 'Enterprise PoE CCTV System',
    description: 'Designed and deployed a robust high-performance Power-over-Ethernet surveillance network with structured cabling for industrial warehouse surveillance, ensuring full security coverage.',
    image: poe,
    year: '2025',
    category: 'CCTV',
    tags: ['PoE System', 'Structured Cabling', 'Security Architecture'],
  },
  {
    title: 'Smartphone Battery Restoration',
    description: 'Conducted high-precision hardware diagnostics and disassembly to replace depleted Li-ion battery cells in premium flagship smartphones, restoring maximum battery health.',
    image: battery,
    year: '2024',
    category: 'REPAIR',
    tags: ['Battery Cell', 'Diagnostics', 'Precision Repair'],
  },
  {
    title: 'Lambang Rattan Company Profile',
    description: 'A modern online showcase and product catalog platform for premium rattan and wooden craft manufacturer, presenting high-end hand-made furniture globally.',
    image: lambang,
    year: '2025',
    category: 'WEBSITE',
    tags: ['PHP', 'Tailwind CSS', 'Vue.js', 'MySQL', 'JavaScript'],
    features: ['Integrated Database'],
  },
  {
    title: 'NVR Server Deployment',
    description: 'Configured and rack-mounted an enterprise Network Video Recorder central server with advanced IP routing, static gateway access, and remote viewing optimization.',
    image: server,
    year: '2025',
    category: 'CCTV',
    tags: ['NVR Installation', 'Server Config', 'IP Routing'],
  },
  {
    title: 'Kapika Woodfest Website',
    description: 'An interactive event landing page and online registration portal built for a regional woodcraft community festival, optimizing attendee registration workflows.',
    image: kapika,
    year: '2025',
    category: 'WEBSITE',
    tags: ['HTML5', 'Vanilla CSS', 'JavaScript', 'PHP', 'MySQL'],
    features: ['Email Automation (PHP-Mailler)', 'Integrated Database'],
  },
  {
    title: 'Optics Fine-Tuning & Align',
    description: 'Performed optical focusing, hardware sensor calibrations, and customized weather-resistant cable jumper repairs for high-altitude outdoor IP surveillance cameras.',
    image: camera,
    year: '2025',
    category: 'CCTV',
    tags: ['IP Camera', 'Focus Tuning', 'Calibration'],
  },
  {
    title: 'Flagship Screen Replacement',
    description: 'Executed delicate glass restoration and OLED panel assembly replacements utilizing micro-soldering techniques, liquid adhesives, and watertight gaskets.',
    image: lcd,
    year: '2023',
    category: 'REPAIR',
    tags: ['OLED Assembly', 'Waterproof Seal', 'Precision Work'],
  },
  {
    title: 'MyService Profile Website',
    description: 'A robust ticket dispatch management portal and real-time technician workload dashboard, optimizing daily customer support workflows.',
    image: myservice,
    year: '2024',
    category: 'WEBSITE',
    tags: ['Vue.js', 'Node.js', 'Tailwind CSS', 'JavaScript'],
    features: ['Integrated Telegram Bot (Notification)'],
  },
  {
    title: 'DVR Enterprise Storage Upgrade',
    description: 'Upgraded storage infrastructure inside multi-channel DVR setups using surveillance-grade enterprise HDDs, optimizing video retention schedules.',
    image: dvr,
    year: '2024',
    category: 'CCTV',
    tags: ['HDD Upgrade', 'Storage Server', 'RAID Data'],
  }
]

const filteredProjects = computed(() => {
  if (activeCategory.value === 'ALL') {
    return projects
  }
  return projects.filter(p => p.category === activeCategory.value)
})

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  // Animate the "- Projects -" subhead
  gsap.fromTo('#projects span.text-\\[12px\\]', 
    { y: 30, opacity: 0 },
    {
      y: 0,
      opacity: 1,
      duration: 0.8,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '#projects',
        start: 'top 50%',
        toggleActions: 'play none none none'
      }
    }
  )

  // Animate the category filter pills container
  gsap.fromTo('#projects .flex-wrap', 
    { y: 30, opacity: 0 },
    {
      y: 0,
      opacity: 1,
      duration: 0.8,
      ease: 'power3.out',
      delay: 0.15,
      scrollTrigger: {
        trigger: '#projects',
        start: 'top 50%',
        toggleActions: 'play none none none'
      }
    }
  )

  // Stagger reveal the initial visible grid card elements
  gsap.fromTo('#projects .project-card', 
    { y: 55, opacity: 0 },
    {
      y: 0,
      opacity: 1,
      duration: 1,
      stagger: 0.15,
      ease: 'power4.out',
      delay: 0.3,
      scrollTrigger: {
        trigger: '#projects',
        start: 'top 50%',
        toggleActions: 'play none none none'
      }
    }
  )
})
</script>

<style scoped>
/* Smooth dynamic staggered layout transition animations for filtering items */
.project-grid-move,
.project-grid-enter-active,
.project-grid-leave-active {
  transition: all 0.6s cubic-bezier(0.25, 1, 0.5, 1);
}

.project-grid-enter-from {
  opacity: 0;
  transform: scale(0.92) translateY(30px);
}

.project-grid-leave-to {
  opacity: 0;
  transform: scale(0.92) translateY(30px);
}

/* Prevent layout overlapping during transitions by positioning leaving cards absolute */
.project-grid-leave-active {
  position: absolute;
  /* width should correspond to the grid columns width including gaps */
  width: calc(33.333% - 20px);
}

@media (max-width: 1279px) {
  .project-grid-leave-active {
    width: calc(50% - 16px);
  }
}

@media (max-width: 767px) {
  .project-grid-leave-active {
    position: static;
    width: 100%;
  }
}
</style>