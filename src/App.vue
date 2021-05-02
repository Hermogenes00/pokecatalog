<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h4 class="is-size-4">Pokedex</h4>
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
        class="button is-fullwidth mt-1 has-background-primary has-text-white"
        @click="buscar"
      >
        Buscar
      </button>

      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <pokemon :name="poke.name" :num="index + 1" :url="poke.url" />
      </div>
    </div>
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
      filteredPokemons:[],
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
  methods:{
    buscar:function(){
      this.filteredPokemons = this.pokemons
      if (this.busca == "" || this.busca == " ") {
        this.pokemons = this.filteredPokemons
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon=>pokemon.name==this.busca)
      }
    }
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
