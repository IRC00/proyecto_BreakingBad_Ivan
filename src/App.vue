<template>
  <body class="h-screen bg-green-900">
    <div class="flex flex-col">
      <div class="flex flex-row bg-green-600">
        <div class="flex-none sm:w-32 w-14">
          <img src="./multimedia/logo_bb.jpg" />
        </div>
        <div class="flex-auto m-auto">
          <h1
            class="text-2xl md:text-5xl sm:text-4xl text-center font-bold text-green-900"
          >
            BreakingBad
          </h1>
        </div>
        <div class="m-auto">
          <Entrada
            @enviaFiltro="cargarPersonajes"
            @enviaSenal="verFavoritos"
            :cargando="this.cargando"
          />
        </div>
      </div>
    </div>
    <div class="flex flex-wrap">
      <ListaPersonajes
        :listaPersonajes="this.lista"
        :favoritos="this.favoritos"
      />
    </div>
  </body>
</template>

<script>
import axios from "axios";
import Entrada from "./components/Entrada.vue";
import ListaPersonajes from "./components/ListaPersonajes.vue";
import "./assets/style.css";
export default {
  components: {
    Entrada,
    ListaPersonajes,
  },
  name: "App",
  data() {
    return {
      lista: [],
      favoritos: false,
      cargando: false,
    };
  },
  methods: {
    // Cargar Pokemons
    async cargarPersonajes(nombre) {
      this.cargando = true;
      try {
        // Hacer una petición a la API con Axios
        const response = await axios.get(
          `https://www.breakingbadapi.com/api/characters?name=${nombre}`
        );
        // Guardar los datos en mi modelo de datos
        this.lista = response.data;
        if (this.lista.length == 0) {
          alert("El personaje a buscar no existe");
        }
        this.search = "";
        this.cargando = false;
        this.favoritos = false;
      } catch (error) {
        console.log(error);
      }
    },
    verFavoritos() {
      this.favoritos = true;
    },
  },
};
</script>
