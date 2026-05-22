<template>
  <div v-if="!isTouchDevice" class="custom-cursor-container pointer-events-none fixed inset-0 z-[999999]">
    <!-- Outer technology reticle follower -->
    <div 
      ref="cursorOuter" 
      class="cursor-outer fixed top-0 left-0 w-10 h-10 pointer-events-none -translate-x-1/2 -translate-y-1/2 mix-blend-difference"
    >
      <!-- Rotating tech HUD structure with bold reinforced lines -->
      <div 
        ref="techReticle"
        class="tech-reticle w-full h-full rounded-full border-2 border-[#a3a3a3]/60 relative flex items-center justify-center transition-all duration-300"
      >
        <!-- Reinforced reticle crosshair ticks -->
        <span class="tick tick-t w-[2px] h-2.5 bg-[#a3a3a3] absolute top-0 left-1/2 -translate-x-1/2 rounded-full"></span>
        <span class="tick tick-b w-[2px] h-2.5 bg-[#a3a3a3] absolute bottom-0 left-1/2 -translate-x-1/2 rounded-full"></span>
        <span class="tick tick-l w-2.5 h-[2px] bg-[#a3a3a3] absolute left-0 top-1/2 -translate-y-1/2 rounded-full"></span>
        <span class="tick tick-r w-2.5 h-[2px] bg-[#a3a3a3] absolute right-0 top-1/2 -translate-y-1/2 rounded-full"></span>
        
        <!-- Reinforced inner dashed circle for rich tech details -->
        <div class="w-[65%] h-[65%] rounded-full border-[1.5px] border-dashed border-[#a3a3a3]/40"></div>
      </div>
    </div>
    
    <!-- Inner glowing target dot -->
    <div 
      ref="cursorInner" 
      class="cursor-inner fixed top-0 left-0 w-2 h-2 rounded-full bg-[#a3a3a3] shadow-[0_0_12px_rgba(163,163,163,0.9)] pointer-events-none -translate-x-1/2 -translate-y-1/2 mix-blend-difference"
    ></div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'

const cursorOuter = ref(null)
const cursorInner = ref(null)
const techReticle = ref(null)
const isTouchDevice = ref(false)

const onMouseMove = (e) => {
  const { clientX: x, clientY: y } = e
  
  // Instant response for inner glowing dot
  gsap.to(cursorInner.value, {
    x: x,
    y: y,
    duration: 0.08,
    ease: 'power2.out'
  })
  
  // Spring delay follower response for outer HUD reticle
  gsap.to(cursorOuter.value, {
    x: x,
    y: y,
    duration: 0.38,
    ease: 'power3.out'
  })
}

// Hover state on interactive elements (Links, buttons, etc.)
const addHoverState = () => {
  // Reticle expands and gets higher contrast
  gsap.to(cursorOuter.value, {
    scale: 1.55,
    duration: 0.3,
    ease: 'power2.out'
  })
  
  gsap.to(techReticle.value, {
    borderColor: 'rgba(163, 163, 163, 0.95)',
    backgroundColor: 'rgba(163, 163, 163, 0.15)',
    borderWidth: '2px',
    duration: 0.3
  })
  
  // Outer ticks expand and gain prominence on hover
  gsap.to('.tick', {
    scale: 1.25,
    opacity: 0.85,
    duration: 0.3
  })

  // Inner dot targets and contracts slightly
  gsap.to(cursorInner.value, {
    scale: 0.6,
    opacity: 0.6,
    duration: 0.2
  })
}

// Reset cursor on mouse leave
const removeHoverState = () => {
  gsap.to(cursorOuter.value, {
    scale: 1,
    duration: 0.3,
    ease: 'power2.out'
  })
  
  gsap.to(techReticle.value, {
    borderColor: 'rgba(163, 163, 163, 0.6)',
    backgroundColor: 'transparent',
    borderWidth: '2px',
    duration: 0.3
  })
  
  gsap.to('.tick', {
    scale: 1,
    opacity: 1,
    duration: 0.3
  })

  gsap.to(cursorInner.value, {
    scale: 1,
    opacity: 1,
    duration: 0.2
  })
}

// Quick HUD pulse compression on mouse click
const onMouseDown = () => {
  gsap.to(cursorOuter.value, {
    scale: 0.72,
    duration: 0.15,
    ease: 'power2.out'
  })
  gsap.to(techReticle.value, {
    borderStyle: 'dashed',
    duration: 0.1
  })
}

// Restore HUD shape on mouse release
const onMouseUp = () => {
  gsap.to(cursorOuter.value, {
    scale: 1.15,
    duration: 0.15,
    ease: 'power2.out',
    onComplete: () => {
      gsap.to(cursorOuter.value, {
        scale: 1,
        duration: 0.15,
        ease: 'power2.out'
      })
    }
  })
  gsap.to(techReticle.value, {
    borderStyle: 'solid',
    duration: 0.15
  })
}

onMounted(() => {
  // Check if coarse pointer (touch device like phone or tablet)
  isTouchDevice.value = window.matchMedia('(pointer: coarse)').matches
  if (isTouchDevice.value) return

  window.addEventListener('mousemove', onMouseMove)
  window.addEventListener('mousedown', onMouseDown)
  window.addEventListener('mouseup', onMouseUp)

  // Scan and attach hover animations to interactive targets
  const attachHoverListeners = () => {
    const targets = document.querySelectorAll('a, button, [role="button"], .project-card, .skill-card, input, textarea, select')
    targets.forEach(target => {
      target.removeEventListener('mouseenter', addHoverState)
      target.removeEventListener('mouseleave', removeHoverState)
      target.addEventListener('mouseenter', addHoverState)
      target.addEventListener('mouseleave', removeHoverState)
    })
  }

  // Trigger scanning initially
  attachHoverListeners()

  // Keep tracking dynamic changes in Vue DOM (e.g. filters)
  const observer = new MutationObserver(attachHoverListeners)
  observer.observe(document.body, { childList: true, subtree: true })

  onUnmounted(() => {
    window.removeEventListener('mousemove', onMouseMove)
    window.removeEventListener('mousedown', onMouseDown)
    window.removeEventListener('mouseup', onMouseUp)
    observer.disconnect()
  })
})
</script>

<style scoped>
.cursor-outer, .cursor-inner {
  will-change: transform;
  z-index: 999999;
}

/* Continuous high tech slow spin animation for reticle follower */
.tech-reticle {
  animation: tech-spin 12s linear infinite;
  transform-origin: center center;
}

@keyframes tech-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
