<template>
  <div class="flex flex-row flex-wrap gap-5 justify-center">
    <Personaje
      v-if="favoritos"
      v-for="personaje in listaFavoritos"
      :personaje="personaje"
      :cambiarTexto="'Eliminar favorito'"
      @enviaEvento="eliminarFavorito(personaje)"
    />
    <Personaje
      v-else="!favoritos"
      v-for="personaje in listaPersonajes"
      :personaje="personaje"
      :cambiarTexto="comprobarFavorito(personaje)"
      @enviaEvento="ejecutarAnadirOEliminar(personaje)"
    />
  </div>
</template>
<script>
import Personaje from "@/components/Personaje.vue";
export default {
  name: "ListaPersonajes",
  data() {
    return {
      listaFavoritos: [],
    };
  },
  components: {
    Personaje,
  },
  props: {
    listaPersonajes: {
      type: Array,
      required: true,
    },
    favoritos: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    anadirFavorito(personaje) {
      if (
        this.listaFavoritos.filter((el) => el.name == personaje.name).length ==
        0
      ) {
        alert("Se ha añadido a " + personaje.name + " a la lista de favoritos");
        this.listaFavoritos.push(personaje);
      } else {
        alert(
          "El personaje " + personaje.name + " ya esta en la lista de favoritos"
        );
      }
    },
    eliminarFavorito(personaje) {
      if (this.listaFavoritos.filter((el) => el.name == personaje.name)) {
        alert("Se ha eliminado a " + personaje.name + " de favoritos");
        this.listaFavoritos = this.listaFavoritos.filter(
          (el) => el.name != personaje.name
        );
      }
    },
    ejecutarAnadirOEliminar(personaje) {
      if (this.comprobarFavorito(personaje) == "Añadir a favorito") {
        this.anadirFavorito(personaje);
      } else {
        this.eliminarFavorito(personaje);
      }
    },
    comprobarFavorito(personaje) {
      if (
        this.listaFavoritos.filter((el) => el.name == personaje.name).length ==
        0
      ) {
        return "Añadir a favorito";
      } else {
        return "Eliminar favorito";
      }
    },
  },
};
</script>
