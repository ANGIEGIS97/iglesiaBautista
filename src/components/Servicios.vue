<template>
  <section
    class="container border-2 mt-4 rounded-lg dark:bg-slate-600 dark:border-slate-600 mx-auto transition duration-300 ease-in-out"
    id="servicio"
  >
    <article>
      <h1
        class="text-gray-800 text-center sm:text-3xl text-2xl font-medium pt-4 dark:text-white"
      >
        Servicio
      </h1>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 p-8">
        <div>
          <img
            src="src/images/servicio/servicio.jpg"
            class="w-full shadow-1-strong rounded mb-4 hover:scale-[1.01]"
            alt="Servicio 1"
          />
          <img
            src="src/images/servicio/servicio1.jpg"
            class="w-full shadow-1-strong rounded mb-4 hover:scale-[1.01]"
            alt="Servicio 2"
          />
        </div>
        <div>
          <img
            src="src/images/servicio/servicio2.jpg"
            class="w-full shadow-1-strong rounded mb-4 hover:scale-[1.01]"
            alt="Servicio 3"
          />
          <img
            src="src/images/servicio/servicio3.jpg"
            class="w-full shadow-1-strong rounded mb-4 hover:scale-[1.01]"
            alt="Servicio 4"
          />
        </div>
        <div>
          <img
            src="src/images/servicio/servicio4.jpg"
            class="w-full shadow-1-strong rounded mb-4 hover:scale-[1.01]"
            alt="Servicio 5"
          />
          <img
            src="src/images/servicio/servicio5.jpg"
            class="w-full shadow-1-strong rounded mb-4 hover:scale-[1.01]"
            alt="Servicio 6"
          />
        </div>
      </div>

      <div
        class="bg-gray-100 rounded-lg mb-4 dark:bg-slate-600 dark:text-white mx-8 border"
      >
        <h3 class="text-2xl text-center p-4">
          Iglesia Bautista su Gracia es Mayor les invita al servicio de
          predicación todos los domingos a las 10:00am <br />
          en el salón comunal Asovivir de Bosa
        </h3>
      </div>

      <!-- Versiculos dinamicos -->
      <blockquote
        class="border-l-4 border-teal-400 italic my-8 mx-8 pl-8 md:pl-12 text-lg dark:text-white"
        id="dailyVersesWrapper"
      ></blockquote>
    </article>
  </section>
</template>
<script>
export default {
  mounted() {
    this.loadDailyVerseScript();
  },
  methods: {
    loadDailyVerseScript() {
      const script = document.createElement("script");
      script.src = "https://dailyverses.net/get/random.js?language=nvi";
      script.async = true;
      script.defer = true;
      document.body.appendChild(script);
    },
  },
};
</script>
