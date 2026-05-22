<template>
  <nav id="navbar" class="fixed top-0 w-full z-150 transition-all duration-500 px-6 py-2 flex justify-between items-center uppercase text-[10px] tracking-[0.3em] font-medium text-black">
    <a href="#" class="text-[20px] tracking-widest font-normal">WHOAMI</a>
    <div class="hidden lg:flex gap-8 text-[13px]">
        <a href="#home" class="hover:text-gray-500 hover:text-shadow-sm transition font-normal duration-300">Home</a>
        <a href="#about" class="hover:text-gray-500 hover:text-shadow-sm transition font-normal duration-300">About</a>
        <a href="#skills" class="hover:text-gray-500 hover:text-shadow-sm transition font-normal duration-300">Skills</a>
        <a href="#projects" class="hover:text-gray-500 hover:text-shadow-sm transition font-normal duration-300">Projects</a>
        <a href="#contact" class="hover:text-gray-500 hover:text-shadow-sm transition font-normal duration-300">Contact</a>
    </div>
    <a 
      href="https://www.instagram.com/s/aGlnaGxpZ2h0OjE4MDExMzEyMjc5NjE0ODQy?igsh=cDloejdheGI0OHE4" 
      target="blank_" 
      class="hidden lg:block text-[13px] font-normal transition duration-300 rounded-md bg-black text-white py-2.75 px-4 border border-transparent hover:bg-transparent hover:text-black hover:border-black">Documentation
    </a>

    <button id="menu-toggle" class="lg:hidden p-2 focus:outline-none relative w-8 h-8 flex flex-col justify-center items-center" @click="toggleMenu">
        <span class="hamburger-line absolute w-6 h-0.5 bg-black transition-all duration-300" style="top: 14px; transform: translateY(-6px)"></span>
        <span class="hamburger-line absolute w-6 h-0.5 bg-black transition-all duration-300" style="top: 50%; transform: translateY(-50%)"></span>
        <span class="hamburger-line absolute w-6 h-0.5 bg-black transition-all duration-300" style="bottom: 14px; transform: translateY(6px)"></span>
    </button>
  </nav>

  <!-- Mobile menu -->
  <div id="mobile-menu" class="fixed inset-0 bg-white z-150 flex flex-col justify-center items-center gap-8 uppercase tracking-[0.2em] -translate-y-full transition-transform duration-700 ease-in-out" :class="{ 'translate-y-0': isMenuOpen }">
    <button id="menu-close" class="absolute top-8 right-8 text-[11px] tracking-widest uppercase hover:opacity-50 transition duration-300" @click="toggleMenu">- Close -</button>
      <a href="#home" class="mobile-link hover:opacity-50 transition duration-300" @click="closeMenu">Home</a>
      <a href="#about" class="mobile-link hover:opacity-50 transition duration-300" @click="closeMenu">About</a>
      <a href="#skills" class="mobile-link hover:opacity-50 transition duration-300" @click="closeMenu">Skills</a>
      <a href="#projects" class="mobile-link hover:opacity-50 transition duration-300" @click="closeMenu">Projects</a>
      <a href="#contact" class="mobile-link hover:opacity-50 transition duration-300" @click="closeMenu">Contact</a>
      <a 
      href="https://www.instagram.com/s/aGlnaGxpZ2h0OjE4MDExMzEyMjc5NjE0ODQy?igsh=cDloejdheGI0OHE4" 
      target="blank_" 
      class="text-[13px] font-normal transition duration-300 rounded-md bg-black text-white py-2.75 px-4 border border-transparent hover:bg-transparent hover:text-black hover:border-black">Documentation
    </a>
  </div>
</template>

<script>
export default {
  name: 'Nav',
  data() {
    return {
      isMenuOpen: false
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
    document.addEventListener('click', this.handleClickOutside);
  },
  unmounted() {
    window.removeEventListener('scroll', this.handleScroll);
    document.removeEventListener('click', this.handleClickOutside);
  },
  methods: {
    handleScroll() {
      const header = document.querySelector('nav');
      if (window.scrollY > 0) {
        header.classList.add('bg-white/15', 'backdrop-blur-lg', 'shadow-md', 'shadow-black/5', 'duration-300', 'py-3');
      } else {
        header.classList.remove('bg-white/15', 'backdrop-blur-lg', 'shadow-md', 'shadow-black/5', 'duration-300', 'py-3');
      }
    },
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
      this.updateHamburgerIcon();
    },
    closeMenu() {
      this.isMenuOpen = false;
      this.updateHamburgerIcon();
    },
    updateHamburgerIcon() {
      const lines = document.querySelectorAll('.hamburger-line');
      if (this.isMenuOpen) {
        // Transform to X shape
        lines[0].style.transform = 'translateY(0) rotate(45deg)';
        lines[1].style.opacity = '0';
        lines[2].style.transform = 'translateY(0) rotate(-45deg)';
      } else {
        // Transform back to hamburger
        lines[0].style.transform = 'translateY(-6px)';
        lines[1].style.opacity = '1';
        lines[2].style.transform = 'translateY(6px)';
      }
    },
    handleClickOutside(event) {
      const menu = document.getElementById('mobile-menu');
      const button = document.getElementById('menu-toggle');
      
      if (this.isMenuOpen && menu && button && !menu.contains(event.target) && !button.contains(event.target)) {
        this.closeMenu();
      }
    }
  }
}
</script>