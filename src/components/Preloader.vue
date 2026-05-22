<template>
  <div v-if="isLoaderActive" class="preloader-wrapper fixed inset-0 z-[99999] overflow-hidden select-none">
    <!-- Sliding exit panels -->
    <div class="preloader-panel fixed inset-0 bg-[#222222] z-1"></div>
    <div class="preloader-panel fixed inset-0 bg-[#e5e5e5] z-2"></div>
    <div class="preloader-panel fixed inset-0 bg-[#0a0a0a] z-3"></div>

    <!-- Main preloader content container -->
    <div class="preloader-content fixed inset-0 z-10 flex flex-col justify-between p-6 md:p-12 text-white">
      <!-- Top header line -->
      <div class="flex justify-between items-center text-[10px] tracking-[0.4em] uppercase opacity-75 font-mono">
        <div class="flex items-center gap-2">
          <span class="w-1.5 h-1.5 rounded-full bg-white animate-pulse"></span>
          <span>IGNATIUS CHRISTIAN</span>
        </div>
        <div class="text-right">
          <span>PORTFOLIO v2.0</span>
        </div>
      </div>

      <!-- Mid center display (Large numbers + Rotating roles) -->
      <div class="flex flex-col md:flex-row md:items-end justify-between gap-8 my-auto">
        <div class="flex flex-col justify-end">
          <div class="h-[20px] overflow-hidden mb-2">
            <Transition name="role-slide" mode="out-in">
              <div 
                :key="activeRole" 
                class="text-xs tracking-[0.3em] uppercase text-gray-400 font-mono font-medium"
              >
                // {{ activeRole }}
              </div>
            </Transition>
          </div>
          <h2 class="text-[25vw] md:text-[16vw] font-light leading-none tracking-tighter font-sans select-none tabular-nums flex items-baseline">
            <span>{{ formattedProgress }}</span>
            <span class="text-lg md:text-2xl font-light opacity-50 ml-2 tracking-normal">%</span>
          </h2>
        </div>

        <div class="max-w-xs md:text-right flex flex-col md:items-end gap-2">
          <div class="text-xs uppercase tracking-widest text-gray-500 font-mono font-medium">
            System Status
          </div>
          <div class="text-sm font-light uppercase tracking-wider text-white font-mono">
            {{ statusText }}
          </div>
        </div>
      </div>

      <!-- Bottom progress line & credits -->
      <div class="flex flex-col gap-6">
        <!-- Thin modern progress bar -->
        <div class="w-full h-[1px] bg-white/10 rounded-full overflow-hidden">
          <div 
            class="h-full bg-white transition-all duration-100 ease-out"
            :style="{ width: `${displayProgress}%` }"
          ></div>
        </div>

        <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4 text-[9px] tracking-widest uppercase opacity-50 font-mono">
          <div>
            <span>DEVELOPMENT & INTEGRATION SYSTEM</span>
          </div>
          <div>
            <span>©{{ new Date().getFullYear() }} ALL RIGHTS RESERVED</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import gsap from 'gsap'

const emit = defineEmits(['loaded'])

const isLoaderActive = ref(true)
const displayProgress = ref(0)
const statusText = ref('INITIALIZING SYSTEM...')

const roles = [
  'WEB DEVELOPMENT',
  'CCTV TECHNICIAN',
  'IT SUPPORT SPECIALIST',
  'PHONE REPAIR ENGINE'
]

const activeRole = computed(() => {
  const segment = 100 / roles.length
  const index = Math.min(
    Math.floor(displayProgress.value / segment),
    roles.length - 1
  )
  return roles[index]
})

const formattedProgress = computed(() => {
  return displayProgress.value < 10 ? `0${displayProgress.value}` : `${displayProgress.value}`
})

// Images from /src/assets
const imagesToPreload = [
  'Christian.jpeg',
  'access-control.jpeg',
  'battery-repair.jpeg',
  'cctv-camera.jpeg',
  'cctv-maintenance.jpeg',
  'cctv-server-installation.jpeg',
  'cctv.jpg',
  'code.jpg',
  'dvr-upgrade-hdd.jpeg',
  'ip-setting.jpeg',
  'it-support.jpg',
  'lcd-repair.jpeg',
  'phone-repair.jpg',
  'poe-installation.jpeg',
  'web-project/coletta.png',
  'web-project/kapikawoodfest.png',
  'web-project/lambangrattan.png',
  'web-project/my-services.png',
  'web-project/MyService-Enterprise.png'
]

const updateStatusText = (progress) => {
  if (progress < 25) {
    statusText.value = 'INITIALIZING ASSETS AND COMPONENTS...'
  } else if (progress < 50) {
    statusText.value = 'LOADING CREATIVE PORTFOLIO MEDIA...'
  } else if (progress < 75) {
    statusText.value = 'CONFIGURING DYNAMIC VIEWPORTS...'
  } else if (progress < 90) {
    statusText.value = 'OPTIMIZING INTERACTIVE ENGINES...'
  } else if (progress < 100) {
    statusText.value = 'FINALIZING SYSTEM SYNC...'
  } else {
    statusText.value = 'LAUNCHING PORFOLIO SYSTEM...'
  }
}

const startLoading = () => {
  let loadedCount = 0
  const totalAssets = imagesToPreload.length
  let assetsLoaded = false
  const progressObj = { value: 0 }

  // Initial GSAP entry animation for preloader elements
  gsap.fromTo('.preloader-content > *', 
    { y: 30, opacity: 0 }, 
    { y: 0, opacity: 1, duration: 1, ease: 'power3.out', stagger: 0.2 }
  )

  // Smooth loading progression over exactly 2.5 seconds.
  // Hold at 90% if assets are not fully loaded.
  const progressTween = gsap.to(progressObj, {
    value: 100,
    duration: 2.5,
    ease: 'power2.out',
    onUpdate: () => {
      const currentVal = Math.floor(progressObj.value)
      
      if (currentVal >= 90 && !assetsLoaded) {
        progressTween.pause()
        displayProgress.value = 90
        updateStatusText(90)
      } else {
        displayProgress.value = currentVal
        updateStatusText(currentVal)
      }
    },
    onComplete: () => {
      triggerExitAnimation()
    }
  })

  // Start preloading assets
  if (totalAssets === 0) {
    assetsLoaded = true
    if (progressTween.paused()) progressTween.play()
    return
  }

  imagesToPreload.forEach((filename) => {
    try {
      // Use Vite's asset URL resolution
      const imgUrl = new URL(`../assets/${filename}`, import.meta.url).href
      const img = new Image()
      img.src = imgUrl
      
      const onAssetLoaded = () => {
        loadedCount++
        if (loadedCount === totalAssets) {
          assetsLoaded = true
          // If paused at 90%, resume!
          if (progressTween && progressTween.paused()) {
            progressTween.play()
          }
        }
      }
      
      img.onload = onAssetLoaded
      img.onerror = onAssetLoaded // prevent stuck state on error
    } catch (e) {
      console.error('Error preloading image:', filename, e)
      loadedCount++
      if (loadedCount === totalAssets) {
        assetsLoaded = true
        if (progressTween && progressTween.paused()) {
          progressTween.play()
        }
      }
    }
  })
}

const triggerExitAnimation = () => {
  const tl = gsap.timeline({
    onComplete: () => {
      emit('loaded')
      isLoaderActive.value = false
    }
  })

  // 1. Stagger fade out the preloader content elements
  tl.to('.preloader-content > *', {
    y: -40,
    opacity: 0,
    duration: 0.8,
    ease: 'power3.in',
    stagger: 0.15
  })

  // 2. Sliding panel staggered exit transitions
  tl.to('.preloader-panel', {
    yPercent: -100,
    duration: 1.2,
    ease: 'power4.inOut',
    stagger: 0.18
  }, '-=0.4')
}

onMounted(() => {
  startLoading()
})
</script>

<style scoped>
/* Staggered transition for roles sliding */
.role-slide-enter-active,
.role-slide-leave-active {
  transition: all 0.5s cubic-bezier(0.25, 1, 0.5, 1);
}

.role-slide-enter-from {
  opacity: 0;
  transform: translateY(12px);
}

.role-slide-leave-to {
  opacity: 0;
  transform: translateY(-12px);
}
</style>
