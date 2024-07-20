<template>
  <div class="container mx-auto px-4 py-8 mt-20">
    <h1
      class="text-3xl text-center sm:text-left sm:text-4xl font-serif mb-4 dark:text-white"
    >
      Preguntas frecuentes
    </h1>
    <p class="text-lg mb-4 dark:text-white">Descubra qué esperar al visitarnos</p>
    <p class="text-gray-600 mb-4 dark:text-white">
      Conozca más sobre nuestros valores y nuestra historia como iglesia
      visitando la página sobre nosotros.
    </p>
    <button
      class="bg-teal-500 text-white hover:bg-teal-400 px-6 py-2 rounded mb-8 transition duration-300 ease-in-out transform hover:scale-105"
    >
      Sobre nosotros
    </button>
    <div class="space-y-6">
      <div
        v-for="(item, index) in preguntas"
        :key="index"
        class="border rounded-lg overflow-hidden shadow-md hover:shadow-lg transition duration-300 ease-in-out"
      >
        <div
          class="h-1 bg-teal-500 transition-all duration-300 ease-in-out"
          :class="{ 'w-full': item.isOpen, 'w-0': !item.isOpen }"
        ></div>
        <button
          @click="toggleItem(index)"
          class="w-full text-left flex justify-between items-center p-4 bg-white dark:bg-gray-800 focus:outline-none"
        >
          <span class="text-sm sm:text-lg font-medium dark:text-white">{{
            item.pregunta
          }}</span>
          <svg
            :class="{ 'rotate-180': item.isOpen }"
            class="w-5 h-5 transition-transform duration-200 text-teal-500"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
              clip-rule="evenodd"
            />
          </svg>
        </button>
        <div
          v-if="item.isOpen"
          class="p-4 bg-gray-50 dark:bg-gray-700 dark:text-white transition-all duration-300 ease-in-out"
        >
          <p>{{ item.respuesta }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      preguntas: [
        {
          pregunta: "1. ¿Cómo se alcanza la salvación?",
          respuesta:
            "La salvación es un don de la gracia de Dios, no es por obras religiosas que podamos hacer. Debemos creer en Jesucristo y recibirlo como nuestro salvador. (Ef.1:8-10; Hch.13:48; Tit. 3:4-7  Efesios 2:8-10)",
          isOpen: false,
        },
        {
          pregunta: "2. ¿Creen en el cielo y en el infierno?",
          respuesta:
            "La Biblia dice que son los únicos lugares después de la muerte. El Cielo es para los salvos y el infierno para los condenados. (Mt.25:31-46; Mt.23:33)",
          isOpen: false,
        },
        {
          pregunta: "3. ¿Cuál es la diferencia entre orar y rezar?",
          respuesta:
            "Orar es conversar con Dios. Nos dirigimos a él como a nuestro Padre, contrariamente, rezar se ha convertido en repeticiones de fórmulas religiosas sin sentido. La oración conocida como el Padre nuestro es realmente una ración modelo. (Mt.6:5-15)",
          isOpen: false,
        },
        {
          pregunta: "4. ¿Qué sacramentos aceptan?",
          respuesta:
            "No tenemos sacramentos. Celebramos dos ordenanzas: La cena del Señor y el bautismo de creyentes. (Hch.2:36-38; 1 Co.11:23-26)",
          isOpen: false,
        },
        {
          pregunta: "5. Creen en la virgen María?",
          respuesta:
            "Sí, pero según la enseñanza de la Biblia. María fue el vaso de honra que Dios usó para la encarnación de su Hijo, pero en ningún momento fue nombrada mediadora entre Dios y los hombres, respetamos su memoria pero no es objeto de adoración. (1 Ti.2:5-6; Lc.1:46-48)",
          isOpen: false,
        },
        {
          pregunta: "6. ¿Por qué no se confiesan?",
          respuesta:
            "Nuestra confesión de pecados es directamente a Dios por medio de Jesucristo nuestro único mediador y salvador. (Heb.4:14-16)",
          isOpen: false,
        },
        {
          pregunta:
            "7.¿Tienen una sede y/o un líder mundial como otras religiones?",
          respuesta:
            "No. Nuestra sede es el local donde nos congregamos y nuestro único jefe es el Señor Jesucristo, y nuestros guías son los pastores que Él ha designado para representarlo (Ef. 4:11-16). Hacemos parte de la Federación de Iglesias Bautistas de Colombia, pero como iglesia local somos autónomos en todo.",
          isOpen: false,
        },
        {
          pregunta:
            " 8. Se dice que ustedes los bautistas no creen en el poder actual del Espíritu Santo ¿por qué?",
          respuesta:
            "Es falso. Necesitamos de la obra del Espíritu Santo para ser regenerados, sin esta obra poderosa y milagrosa nadie puede llegar a ser cristiano. Además, el Espíritu Santo actúa en los creyentes, santificándolos diariamente (Ro. 8:9; 2 Ts. 2:13). El cuerpo del creyente es templo del Espíritu Santo (1 Corintios 3:16).",
          isOpen: false,
        },
        {
          pregunta: "9. ¿Cuál es su posición frente al celibato?",
          respuesta:
            "La Biblia enseña que los pastores pueden casarse y tener hijos. El apóstol Pablo enseñó que el abstenerse de mujer y quedarse soltero es un don especial (1 Co.7:7-9)",
          isOpen: false,
        },
        {
          pregunta: "10. ¿El diezmo es obligatorio?",
          respuesta:
            "No, el diezmo no es obligatorio, es voluntario en respuesta a la gracia de Dios. Hay suficientes pasajes bíblicos que nos enseñan su práctica. La ley mosaica lo establecía sobre los frutos de la tierra y el ganado (Levítico 27:30-35) y era entregado a los levitas para el sustento de ellos (Números 18:21). En Malaquías 3 vemos que era para que hubiera comida para los necesitados. En tiempos del Señor Jesucristo también se aplicaba (Lucas 11:42; Lucas 18:12). Sin embargo, no fue prescrito a la iglesia por el Señor Jesucristo ni por los apóstoles como una norma. Bajo la economía de la gracia, se espera que todo creyente aporte de corazón dispuesto (2 Corintios 9:7), no por norma impuesta, sino presentando el ejemplo del Señor Jesucristo (2 Corintios 8:9). Si fuera por norma, deberíamos dar en muchos casos más de la décima parte (1 Corintios 16:2, ofrenda para los santos).",
          isOpen: false,
        },
        {
          pregunta:
            "11. Hay muchos pastores millonarios ¿la religión es un negocio?",
          respuesta:
            "No debería serlo. Lamentablemente, muchos pastores han convertido la Iglesia en una empresa lucrativa y un negocio para sí mismos. No son iglesias del Señor Jesucristo quienes lo hacen. Por otra parte, las iglesias deben ser responsables de sostener generosamente a sus pastores (2 P. 2:1-3; 1 Ti. 5:17-18).",
          isOpen: false,
        },
      ],
    };
  },
  methods: {
    toggleItem(index) {
      this.preguntas[index].isOpen = !this.preguntas[index].isOpen;
    },
  },
};
</script>
