<template>
  <div id="app">
    <div class="container">
      <h2 class="is-size-2">Pokedex</h2>
      <h5>Bem vindo ao meu catálogo de pokemons, divirta-se!!!</h5>
      <hr />

      <input
        type="text"
        name=""
        class="input"
        placeholder="Procure por um pokemon"
        v-model="busca"
        id=""
      />

      <button
        id="buscaBtn"
        class="button is-fullwidth mt-3 has-background-primary has-text-white"
        @click="buscar"
      >
        Buscar
      </button>

      <div class="columns is-multiline is-mobile">
        <div
          class="column is-4"
          v-for="(poke, index) in filteredPokemons"
          :key="poke.url"
        >
          <pokemon :name="poke.name" :num="index + 1" :url="poke.url" />
        </div>
      </div>
    </div>
    <!--Fechou container-->
<footer class="footer">
  <div class="content has-text-centered">
    <p>
      <strong>Projeto desenvolvido por Hermógenes Neto</strong><br>      
       <a href="https://github.com/Hermogenes00">Github</a> | <a href="https://www.linkedin.com/in/hermogenesneto/">LinkedIn</a> <br>
    </p>
  </div>
</footer>

    <!--Footer-->

  </div>
</template>


<script>
import axios from "axios";
import pokemon from "./components/pokemon";

export default {
  name: "App",
  components: {
    pokemon,
  },
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((response) => {
        let data = response.data;
        this.pokemons = data.results;
        this.filteredPokemons = data.results;
      })
      .catch((err) => console.log(err));
  },
  methods: {
    buscar: function () {
      this.filteredPokemons = this.pokemons;
      if (this.busca == "" || this.busca == " ") {
        this.pokemons = this.filteredPokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name == this.busca
        );
      }
    },
  },
  computed: {
    // resultadoBusca: function () {
    //   if (this.busca == "" || this.busca == " ") {
    //     return this.pokemons;
    //   } else {
    //     return this.pokemons.filter((pokemon) => {
    //       return pokemon.name == this.busca;
    //     });
    //   }
    // },
  },
};
</script>




<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
