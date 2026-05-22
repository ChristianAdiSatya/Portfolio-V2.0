<template>
  <!-- Modern Typographic Editorial Footer -->
  <footer id="contact" class="relative bg-black pt-24 pb-16 px-6 lg:px-14 border-t border-neutral-900 overflow-hidden">
    
    <!-- 1. Infinite Horizontal Scrolling Marquee Banner (Placed outside max-w-full to stretch fully to left and right viewport edges) -->
    <div class="w-[calc(100%+3rem)] lg:w-[calc(100%+7rem)] -mx-6 lg:-mx-14 overflow-hidden bg-neutral-950/80 border-y border-neutral-900 py-6 mb-20 select-none">
      <div class="animate-marquee flex whitespace-nowrap gap-12 text-[10px] font-mono tracking-[0.4em] uppercase text-neutral-500 font-light">
        <span>• GET IN TOUCH • WEB DEVELOPER • CCTV SYSTEMS • IT SUPPORT • SMARTPHONE REPAIRS •</span>
        <span>• GET IN TOUCH • WEB DEVELOPER • CCTV SYSTEMS • IT SUPPORT • SMARTPHONE REPAIRS •</span>
        <span>• GET IN TOUCH • WEB DEVELOPER • CCTV SYSTEMS • IT SUPPORT • SMARTPHONE REPAIRS •</span>
        <span>• GET IN TOUCH • WEB DEVELOPER • CCTV SYSTEMS • IT SUPPORT • SMARTPHONE REPAIRS •</span>
      </div>
    </div>

    <div class="max-w-full mx-auto">
      
      <!-- 2. Main Footer Content Grid -->
      <div class="grid lg:grid-cols-12 gap-16 lg:gap-20">
        
        <!-- Left Side: Bold CTA and Large Interactive Contacts -->
        <div class="lg:col-span-7 flex flex-col justify-between">
          <div>
            <h2 class="text-white text-4xl sm:text-5xl lg:text-7xl font-semibold tracking-tight leading-[1.05] mb-16 uppercase">
              Let's build<br />something great.
            </h2>
            
            <div class="space-y-8">
              <!-- Email Line -->
              <div>
                <p class="text-[9px] font-mono tracking-[0.3em] uppercase text-neutral-600 mb-2 font-medium">01 / Email</p>
                <a
                  href="mailto:casatya82@gmail.com"
                  target="_blank"
                  class="group relative inline-block text-white font-normal text-lg sm:text-xl lg:text-2xl transition duration-300 select-all"
                >
                  casatya82@gmail.com
                  <span class="absolute bottom-0 left-0 w-0 h-[1px] bg-white transition-all duration-300 group-hover:w-full"></span>
                </a>
              </div>
              
              <!-- Whatsapp Line -->
              <div>
                <p class="text-[9px] font-mono tracking-[0.3em] uppercase text-neutral-600 mb-2 font-medium">02 / Whatsapp</p>
                <a 
                  href="https://api.whatsapp.com/send?phone=6281392991442&amp;text=Halo, Christian!" 
                  target="_blank"
                  class="group relative inline-block text-white font-normal text-lg sm:text-xl lg:text-2xl transition duration-300"
                >
                  +62 813 9299 1442
                  <span class="absolute bottom-0 left-0 w-0 h-[1px] bg-white transition-all duration-300 group-hover:w-full"></span>
                </a>
              </div>
            </div>
          </div>
        </div>

        <!-- Right Side: Numbered Navigation and Social Links -->
        <div class="lg:col-span-5 flex flex-col justify-end">
          <div class="grid grid-cols-2 gap-12">
            
            <!-- Numbered Navigation List -->
            <div>
              <h5 class="text-[10px] font-mono uppercase tracking-[0.3em] text-neutral-600 mb-8 font-medium">
                Navigation
              </h5>
              <ul class="space-y-4">
                <li v-for="(link, i) in navigationLinks" :key="link.href" class="font-mono text-xs uppercase tracking-widest">
                  <a 
                    :href="link.href" 
                    class="group text-neutral-400 hover:text-white transition duration-300 flex items-center gap-3"
                  >
                    <span class="text-[9px] text-neutral-700 font-light group-hover:text-white transition-colors duration-300">0{{ i + 1 }}</span>
                    <span>{{ link.label }}</span>
                  </a>
                </li>
              </ul>
            </div>
            
            <!-- Numbered Social List -->
            <div>
              <h5 class="text-[10px] font-mono uppercase tracking-[0.3em] text-neutral-600 mb-8 font-medium">
                Follow Me
              </h5>
              <ul class="space-y-4">
                <li v-for="(link, i) in socialLinks" :key="link.url" class="font-mono text-xs uppercase tracking-widest">
                  <a 
                    :href="link.url" 
                    target="_blank" 
                    class="group text-neutral-400 hover:text-white transition duration-300 flex items-center gap-3"
                  >
                    <span class="text-[9px] text-neutral-700 font-light group-hover:text-white transition-colors duration-300">/ 0{{ i + 1 }}</span>
                    <span>{{ link.name }}</span>
                  </a>
                </li>
              </ul>
            </div>

          </div>
        </div>

      </div>

      <!-- 3. Bottom Bar: Copyright and Branded Signature Logo -->
      <div class="w-full mt-24 pt-10 border-t border-neutral-900 flex flex-col md:flex-row justify-between items-center gap-8">
        <p class="text-neutral-600 text-[10px] font-mono uppercase tracking-[0.3em] font-light">
          © 2026 Christian Adi Satya. All Rights Reserved.
        </p>
        
        <div class="text-[12px] font-mono uppercase tracking-[0.4em] text-neutral-700 select-none font-medium">
          CHRISTIAN ADI SATYA
        </div>
      </div>

    </div>
  </footer>
</template>

<script setup>
import { onMounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

const navigationLinks = [
  { label: 'Home', href: '#home' },
  { label: 'About', href: '#about' },
  { label: 'Skills', href: '#skills' },
  { label: 'Projects', href: '#projects' },
  { label: 'Contact', href: '#contact' },
  { label: 'My Services', href: 'https://my-services-kappa.vercel.app/', target: '_blank', rel: 'noopener noreferrer'}
]

const socialLinks = [
  { name: 'Instagram', url: 'https://www.instagram.com/whoammi_/' },
  { name: 'Facebook', url: 'https://www.facebook.com/christian.adi.334' },
  { name: 'LinkedIn', url: 'https://www.linkedin.com/in/christian-adi-satya' }
]

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  // Animate the main CTA "Let's build something great."
  gsap.fromTo('#contact h2', 
    { y: 50, opacity: 0 },
    {
      y: 0,
      opacity: 1,
      duration: 1,
      ease: 'power3.out',
      scrollTrigger: {
        trigger: '#contact',
        start: 'top 85%',
        toggleActions: 'play none none none'
      }
    }
  )

  // Animate Email & WhatsApp lines
  gsap.fromTo('#contact .space-y-8 > div',
    { y: 30, opacity: 0 },
    {
      y: 0,
      opacity: 1,
      duration: 0.8,
      stagger: 0.15,
      ease: 'power3.out',
      delay: 0.25,
      scrollTrigger: {
        trigger: '#contact',
        start: 'top 85%',
        toggleActions: 'play none none none'
      }
    }
  )

  // Animate Navigation & Social List columns
  gsap.fromTo('#contact .grid-cols-2 > div',
    { y: 35, opacity: 0 },
    {
      y: 0,
      opacity: 1,
      duration: 0.8,
      stagger: 0.15,
      ease: 'power3.out',
      delay: 0.4,
      scrollTrigger: {
        trigger: '#contact',
        start: 'top 85%',
        toggleActions: 'play none none none'
      }
    }
  )

  // Animate Copyright & Branded Signature Logo
  gsap.fromTo('#contact .border-t-neutral-900 > *',
    { y: 20, opacity: 0 },
    {
      y: 0,
      opacity: 1,
      duration: 0.8,
      stagger: 0.15,
      ease: 'power3.out',
      delay: 0.6,
      scrollTrigger: {
        trigger: '#contact',
        start: 'top 90%',
        toggleActions: 'play none none none'
      }
    }
  )
})
</script>

<style scoped>
/* Infinite Horizontal Marquee Scrolling Animation */
@keyframes marquee {
  0% {
    transform: translateX(0%);
  }
  100% {
    transform: translateX(-50%);
  }
}

.animate-marquee {
  display: flex;
  width: max-content;
  animation: marquee 30s linear infinite;
}

/* Ensure smooth Hardware Acceleration for 60fps scrolling */
.animate-marquee span {
  flex-shrink: 0;
  will-change: transform;
}
</style>