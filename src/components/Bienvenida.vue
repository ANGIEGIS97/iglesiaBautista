<template>
  <div>
    <!-- Hero -->
    <div class="relative h-screen overflow-hidden">
      <div
        ref="parallaxBackground"
        class="absolute top-0 left-0 w-full h-full bg-cover bg-center"
        :style="{ backgroundImage: `url(${heroImage})` }"
      ></div>
      <div class="absolute inset-0 bg-black opacity-50"></div>
      <div class="relative h-full flex items-center justify-center z-10">
        <div class="text-center text-white p-5 selection:bg-teal-500">
          <h1 class="text-4xl sm:text-5xl font-bold mb-4">
            Bienvenido a nuestra iglesia
          </h1>
          <p class="text-xl sm:text-2xl">
            Un lugar de fe, comunidad y crecimiento espiritual
          </p>
        </div>
      </div>

      <!-- Scroll Indicator -->
      <div class="absolute bottom-10 left-1/2 transform -translate-x-1/2 z-20">
        <div class="scroll-indicator">
          <span class="text-white text-sm mb-2">Bajar</span>
          <div class="w-6 h-10 border-2 border-white rounded-full p-1">
            <div
              class="w-1 h-3 bg-white rounded-full animate-bounce mx-auto"
            ></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      heroImage: "https://i.ibb.co/vCWvVYb/principal.jpg",
    };
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll() {
      const parallaxBackground = this.$refs.parallaxBackground;
      if (parallaxBackground) {
        const scrollPosition = window.pageYOffset;
        const limit = parallaxBackground.offsetHeight;
        if (scrollPosition <= limit) {
          parallaxBackground.style.transform = `translateY(${
            scrollPosition * 0.5
          }px)`;
        }
      }
    },
  },
};
</script>

<style scoped>
.overflow-hidden {
  overflow: hidden;
}

.scroll-indicator {
  display: flex;
  flex-direction: column;
  align-items: center;
  animation: fadeInOut 2s infinite;
}

@keyframes fadeInOut {
  0%,
  100% {
    opacity: 0.5;
  }
  50% {
    opacity: 1;
  }
}
</style>
