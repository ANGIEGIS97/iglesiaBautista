<template>
  <div
    class="bg-gray-100 dark:bg-slate-600 px-2 sm:px-20 py-6 container mx-auto transition duration-300 ease-in-out"
  >
    <h2 class="text-2xl font-bold mb-8 dark:text-white sm:-ml-8">
      Próximos eventos
    </h2>

    <!-- Estado de carga -->
    <div v-if="cargando" class="flex flex-col justify-center items-center h-64">
      <div class="loader mb-4"></div>
      <p class="text-gray-700 dark:text-gray-300">Cargando eventos...</p>
    </div>

    <!-- Mensaje de error -->
    <div v-else-if="error" class="text-red-500 text-center py-8">
      {{ error }}
    </div>

    <!-- Contenido principal -->
    <div v-else class="relative">
      <swiper
        :modules="modulos"
        :slides-per-view="2"
        :space-between="7"
        :pagination="{ clickable: true }"
        :navigation="false"
        :grab-cursor="true"
        class="mySwiper custom-swiper rounded-lg overflow-hidden"
        :breakpoints="{
          '420': {
            slidesPerView: 2,
            spaceBetween: 20,
          },
          '768': {
            slidesPerView: 3,
            spaceBetween: 20,
          },
          '1020': {
            slidesPerView: 4,
            spaceBetween: 20,
          },
        }"
      >
        <swiper-slide v-for="evento in eventos" :key="evento.fecha">
          <div
            class="bg-white py-4 px-3 sm:px-6 rounded-lg shadow mx-auto mb-10"
          >
            <div class="flex items-center justify-center p-4">
              <div
                class="relative text-3xl font-bold text-black border py-2 px-6 rounded-md shadow-md"
              >
                <div
                  class="absolute top-1 left-3 w-1.5 h-1.5 bg-black rounded-full"
                ></div>
                <div
                  class="absolute top-1 right-3 w-1.5 h-1.5 bg-black rounded-full"
                ></div>
                <div class="text-center">{{ evento.dia }}</div>
                <div class="text-sm text-gray-600 text-center">
                  {{ evento.mes }}
                </div>
              </div>
            </div>
            <h3 class="text-md sm:text-xl font-semibold mb-2">
              {{ evento.titulo }}
            </h3>
            <p class="text-sm text-gray-600 mb-2 flex items-center">
              <i class="fas fa-clock mr-2"></i
              >{{ obtenerDiaSemana(evento.fecha) }}, {{ evento.hora }}
            </p>
            <p class="text-sm text-gray-600 mb-2 flex items-center">
              <i class="fas fa-map-marker-alt mr-2"></i> {{ evento.lugar }}
            </p>
            <p
              class="text-sm font-semibold text-red-600 mb-4 dark:text-teal-600"
            >
              <i class="fas fa-calendar-plus mr-2"></i>
              {{
                evento.diasRestantes === 0
                  ? "Hoy"
                  : evento.diasRestantes === 1
                    ? "1 día restante"
                    : `${evento.diasRestantes} días restantes`
              }}
            </p>
            <button
              @click="abrirModal(evento)"
              class="bg-red-500 text-white px-4 py-2 rounded-lg hover:bg-red-700 transition duration-300 dark:bg-teal-500 dark:hover:bg-teal-700"
            >
              Leer más
            </button>
          </div>
        </swiper-slide>
      </swiper>
    </div>

    <!-- Modal -->
    <div
      v-if="eventoSeleccionado"
      class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50"
    >
      <div class="bg-white p-8 rounded-lg shadow-xl max-w-md w-full">
        <h2 class="text-2xl font-bold mb-4">
          {{ eventoSeleccionado.titulo }}
        </h2>
        <p class="mb-2">
          <strong>Fecha:</strong> {{ eventoSeleccionado.dia }} de
          {{ eventoSeleccionado.mes }}
        </p>
        <p class="mb-2"><strong>Hora:</strong> {{ eventoSeleccionado.hora }}</p>
        <p class="mb-2">
          <strong>Lugar:</strong> {{ eventoSeleccionado.lugar }}
        </p>

        <p class="mb-2">
          <strong>Descripción:</strong> {{ eventoSeleccionado.descripcion }}
        </p>
        <p class="mb-2 text-red-600 dark:text-teal-600">
          <strong>Días restantes:</strong>
          {{
            eventoSeleccionado.diasRestantes === 0
              ? "Hoy"
              : eventoSeleccionado.diasRestantes === 1
                ? "1 día"
                : `${eventoSeleccionado.diasRestantes} días`
          }}
        </p>
        <button
          @click="cerrarModal"
          class="bg-red-500 text-white px-4 py-2 rounded-lg hover:bg-red-700 transition duration-300 dark:bg-teal-500 dark:hover:bg-teal-700"
        >
          Cerrar
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Pagination, Navigation } from "swiper/modules";
import "swiper/css";
import "swiper/css/pagination";
import "swiper/css/navigation";

export default {
  components: {
    Swiper,
    SwiperSlide,
  },
  setup() {
    const eventos = ref([]);
    const eventoSeleccionado = ref(null);
    const cargando = ref(true);
    const error = ref(null);

    const abrirModal = (evento) => {
      eventoSeleccionado.value = evento;
    };

    const cerrarModal = () => {
      eventoSeleccionado.value = null;
    };

    const obtenerDiaSemana = (fecha) => {
      const dias = [
        "Domingo",
        "Lunes",
        "Martes",
        "Miércoles",
        "Jueves",
        "Viernes",
        "Sábado",
      ];
      return dias[fecha.getUTCDay()];
    };

    onMounted(async () => {
      try {
        cargando.value = true;
        const respuesta = await fetch("/eventos.json");
        if (!respuesta.ok) {
          throw new Error("Error al obtener los eventos");
        }
        const datos = await respuesta.json();
        const hoy = new Date();
        hoy.setHours(0, 0, 0, 0);
        eventos.value = datos
          .map((evento) => {
            const [year, month, day] = evento.fecha.split("-").map(Number);
            const fechaEvento = new Date(Date.UTC(year, month - 1, day));
            const diasRestantes = Math.max(
              0,
              Math.floor((fechaEvento - hoy) / (1000 * 60 * 60 * 24))
            );
            return {
              ...evento,
              fecha: fechaEvento,
              dia: fechaEvento.getUTCDate().toString().padStart(2, "0"),
              mes: fechaEvento.toLocaleString("es", {
                month: "long",
                timeZone: "UTC",
              }),
              diasRestantes: diasRestantes,
              diaSemana: obtenerDiaSemana(fechaEvento),
            };
          })
          .filter((evento) => evento.fecha >= hoy)
          .sort((a, b) => a.fecha - b.fecha)
          .slice(0, 10);
      } catch (err) {
        console.error("Error al cargar los eventos:", err);
        error.value =
          "No se pudieron cargar los eventos. Por favor, intente más tarde.";
      } finally {
        cargando.value = false;
      }
    });

    return {
      modulos: [Pagination, Navigation],
      eventos,
      eventoSeleccionado,
      abrirModal,
      cerrarModal,
      cargando,
      error,
      obtenerDiaSemana,
    };
  },
};
</script>
<style scoped>
/* El loader se consigue en https://css-loaders.com/spinner/ */
.loader {
  width: 50px;
  padding: 8px;
  aspect-ratio: 1;
  border-radius: 50%;
  background: #25b09b;
  --_m: conic-gradient(#0000 10%, #000), linear-gradient(#000 0 0) content-box;
  -webkit-mask: var(--_m);
  mask: var(--_m);
  -webkit-mask-composite: source-out;
  mask-composite: subtract;
  animation: l3 1s infinite linear;
}
@keyframes l3 {
  to {
    transform: rotate(1turn);
  }
}
/* Fin del loader */

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
