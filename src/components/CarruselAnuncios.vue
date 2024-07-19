<template>
  <div
    class="container mx-auto sm:p-16 bg-gray-100 rounded-b-xl dark:bg-slate-600 transition duration-300 ease-in-out"
  >
    <swiper
      :slides-per-view="1"
      :space-between="30"
      :navigation="true"
      :pagination="{ clickable: true }"
      :modules="modules"
      :grab-cursor="true"
      class="mySwiper custom-swiper rounded-lg overflow-hidden"
    >
      <swiper-slide v-for="(image, index) in images" :key="index">
        <img
          :src="image"
          :alt="`Slide ${index + 1}`"
          class="w-full h-auto object-cover rounded-lg mb-10"
        />
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
import { Swiper, SwiperSlide } from "swiper/vue";
import { Navigation, Pagination } from "swiper/modules";

import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";

export default {
  components: {
    Swiper,
    SwiperSlide,
  },
  data() {
    return {
      modules: [Navigation, Pagination],
      images: [
        "src/images/carrusel/imagen_1.jpeg",
        "src/images/carrusel/imagen_2.jpeg",
        "src/images/carrusel/imagen_3.jpeg",
        "src/images/carrusel/imagen_4.jpeg",
        "src/images/carrusel/imagen_5.jpeg",
        "src/images/carrusel/imagen_6.jpeg",
      ],
    };
  },
};
</script>

<style lang="postcss">
.custom-swiper {
  .swiper-button-next,
  .swiper-button-prev {
    @apply text-teal-500;
  }

  .swiper-button-next:hover,
  .swiper-button-prev:hover {
    @apply text-teal-400;
  }

  .swiper-pagination-bullet {
    @apply bg-teal-400;
    width: 10px;
    height: 10px;
  }

  .swiper-pagination-bullet-active {
    @apply bg-teal-500;
    width: 10px;
    height: 10px;
  }
}
</style>
