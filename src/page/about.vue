<template>
    <!-- About Section -->
    <section id="about" class="min-h-screen py-30 px-6 lg:px-14 bg-white relative overflow-hidden">
      <div class="max-w-full mx-auto">
        <!-- Unique class to avoid selector collision -->
        <span
          class="text-[12px] uppercase tracking-[0.5em] text-studio-muted mb-12 block about-subhead"
        >- About Me -
        </span>
        <!-- Unique class to avoid selector collision -->
        <h2 class="text-xl lg:text-5xl leading-tight about-main-text tracking-normal font-normal">
          Hi, I’m Ignatius Christian Adi Satya, an IT enthusiast based in Semarang, Indonesia. I have experience in <span class="italic text-gray-500">web developer, CCTV Technician, and IT support</span>, with a focus on practical and efficient solutions. I enjoy learning new technologies, solving technical problems, and delivering reliable results through clear communication and continuous improvement.
        </h2>
        <div class="h-60 w-60 lg:h-100 lg:w-100 2xl:h-125 2xl:w-125 rounded-full mx-auto mt-15 profile-image-container relative">
          <img src="../assets/Christian.jpeg" alt="Christian" class="rounded-full w-full h-full object-cover">
          <div class="max-w-full bg-transparent backdrop-blur-md rounded-md border-black border px-1 py-2 lg:px-2 lg:py-4 -mt-10 quote-box">
            <h4 class="text-lg lg:text-[28px] 2xl:text-3xl leading-tight tracking-wider uppercase text-center about-quote">
              "<span class="text-gray-400 font-light text-shadow-sm italic">Don't Learn Without Error.</span>"
            </h4>
          </div>
        </div>
      </div>
    </section>
</template>

<script setup>
import { onMounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  // Ultra-smooth reveal for the "- About Me -" label
  gsap.fromTo('.about-subhead', 
    { y: 20, opacity: 0 },
    {
      y: 0,
      opacity: 1,
      duration: 1,
      ease: 'power2.out',
      scrollTrigger: {
        trigger: '#about',
        start: 'top 50%',
        toggleActions: 'play none none none'
      }
    }
  )

  // Soft, cinematic fade-in reveal for the main intro text (no popup flashes)
  gsap.fromTo('.about-main-text',
    { y: 30, opacity: 0 },
    {
      y: 0,
      opacity: 1,
      duration: 1.6,
      ease: 'power3.out',
      delay: 0.1,
      scrollTrigger: {
        trigger: '#about',
        start: 'top 50%',
        toggleActions: 'play none none none'
      }
    }
  )

  // Smooth, organic slide and scale for the profile image & quote box
  gsap.fromTo('.profile-image-container',
    { scale: 0.96, y: 40, opacity: 0 },
    {
      scale: 1,
      y: 0,
      opacity: 1,
      duration: 1.8,
      ease: 'power4.out',
      delay: 0.25,
      scrollTrigger: {
        trigger: '.profile-image-container',
        start: 'top 60%',
        toggleActions: 'play none none none'
      }
    }
  )
})
</script>

<style scoped>
/* Pre-hide elements to prevent sudden FOUC pops or flashes before ScrollTrigger fires */
.about-subhead,
.about-main-text,
.profile-image-container {
  opacity: 0;
  will-change: transform, opacity;
}
</style>