<template>
  <div id="header" class="bg-white/70 fixed w-full z-20 top-20">
    <div id="progress" class="h-1.5 shadow" :style="progressStyle"></div>
  </div>
</template>

<script>
import { ref, onMounted, onBeforeUnmount, computed } from "vue";

export default {
  name: "ProgressBar",
  setup() {
    const scroll = ref(0);

    const progressStyle = computed(() => ({
      background: `linear-gradient(to right, #4dc0b5 ${scroll.value}%, transparent 0)`,
    }));

    const handleScroll = () => {
      const { scrollTop, scrollHeight, clientHeight } =
        document.documentElement;
      scroll.value = (scrollTop / (scrollHeight - clientHeight)) * 100;
    };

    onMounted(() => window.addEventListener("scroll", handleScroll));
    onBeforeUnmount(() => window.removeEventListener("scroll", handleScroll));

    return { progressStyle };
  },
};
</script>
