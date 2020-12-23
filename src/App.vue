<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h1 class="title is-1">Pokedex</h1>
      <input
      class="input is-primary" 
      type="text"
      name=""
      id=""
      placeholder="Buscarpokemon..."
      v-model="search"
      >
      <button @click="searchPokemon" class="button is-primary is-fullwidth mt-3" id="buscaBtn">Buscar</button>
      <div >
        <div v-for="(pokemon, index) in filteredPokemons" :key="pokemon.url">
          <Pokemon :name="pokemon.name" :url="pokemon.url"
          :num="index+1"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  components:{
    Pokemon
  },
  data(){
    return{
       pokemons: [],
       filteredPokemons: [],
       search: ''
    }
  },
  created(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
    .then(res => {
      console.log(res.data.results)
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
    })
  },
  methods:{
    searchPokemon(){
      this.filteredPokemons = this.pokemons
        if(this.search == '' || this.search == ' '){
          this.filteredPokemons = this.pokemons
        } else {
          this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.search)
        }
    }
  },
  computed:{
    // resultSearch(){
    //   if(this.search == '' || this.search == ' '){
    //     return this.pokemons
    //   } else {
    //     return this.pokemons.filter(pokemon => pokemon.name == this.search)
    //   }
    // }
  }
}
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
