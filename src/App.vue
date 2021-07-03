<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <br />
      <h4 class="is-size-4">Pokedex</h4>
      <input
        class="input is-rounded"
        type="text"
        placeholder="Buscar pokemon pelo nome"
        v-model="busca"
      />
      <button class="button is-fullwidth is-success" id="buscaBtn" @click="buscar">
        Buscar
      </button>
      <div class="column is-half is-offset-one-quarter">
        <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
          <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
  name: "App",

  data() {
    return {
      pokemons: [],
      busca: "",
      filteredPokemons: []
    };
  },
  created: function() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((response) => {
        this.pokemons = response.data.results;
        this.filteredPokemons = response.data.results
      });
  },
  components: {
    Pokemon,
  },
  methods:{
    buscar: function(){
      this.filteredPokemons = this.pokemons
      if (this.busca == "" || this.busca == " "){
        this.filteredPokemons = this.pokemons
      }
      else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }  
    }
  },
  computed:{
    /* resultadoBusca: function(){
      if (this.busca == "" || this.busca == " "){
        return this.pokemons
      }
      else {
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    } */
  }
};
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

#buscaBtn {
  margin-top: 2%;
}
</style>
