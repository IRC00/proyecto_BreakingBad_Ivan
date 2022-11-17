<template>
  <div
    class="flex flex-col items-center w-96 h-96 bg-white rounded-lg border shadow-md md:flex-row md:max-w-xl hover:bg-gray-100 dark:border-gray-700 dark:bg-gray-800 dark:hover:bg-gray-700"
  >
    <img
      class="object-cover w-24 h-48 md:w-56 md:h-full rounded-t-lg md:rounded-none md:rounded-l-lg"
      :src="personaje.img"
    />
    <div class="flex flex-col justify-between p-4 leading-normal">
      <h5
        class="mb-2 text-1xl md:text-2xl text-center font-bold tracking-tight text-gray-900 dark:text-white"
      >
        {{ personaje.name }}
      </h5>
      <ul
        class="mb-3 text-sm md:text-base font-normal text-gray-700 dark:text-gray-400"
      >
        <li>Ocupacion:</li>
        <ul class="list-disc list-inside">
          <li v-for="ocupacion in personaje.occupation" :key="ocupacion">
            {{ ocupacion }}
          </li>
        </ul>
        <li>Estado: {{ personaje.status }}</li>
        <li>Nacimiento: {{ personaje.birthday }}</li>
      </ul>
      <BotonFavorito @enviaEvento="enviarEvento" :cambiarTexto="cambiarTexto" />
    </div>
  </div>
</template>
<script>
import BotonFavorito from "./BotonFavorito.vue";

export default {
  name: "Personaje",
  //emits: ["enviaEvento"],
  props: {
    personaje: {
      type: Object,
      required: true,
    },
    cambiarTexto: {
      type: String,
      required: true,
    },
  },
  components: {
    BotonFavorito,
  },
  methods: {
    enviarEvento() {
      this.$emit("enviaEvento");
    },
  },
};
</script>
