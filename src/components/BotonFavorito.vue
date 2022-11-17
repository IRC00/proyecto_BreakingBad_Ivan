<template>
  <button
    type="button"
    @click="enviarEvento"
    class="w-52 md:w-32 text-white bg-green-700 hover:bg-green-800 focus:outline-none focus:ring-4 focus:ring-green-300 font-medium rounded-full text-sm px-5 py-2.5 text-center mr-2 mb-2 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800"
  >
    {{ this.cambiarTexto }}
  </button>
</template>
<script>
export default {
  name: "BotonFavorito",
  props: {
    cambiarTexto: {
      type: String,
      required: true,
    },
  },
  methods: {
    enviarEvento() {
      this.$emit("enviaEvento", this.texto);
    },
  },
};
</script>
