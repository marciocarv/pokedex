<template>
  <div id="app">
    
    <div class="columns">
        <div class="column is-half is-offset-one-quarter">
          <img src="./assets/logo.png">
          <p class="is-size-4">Pokedex</p>
          <input class="input is-hovered" type="text" v-model="busca" placeholder="Buscar Pokemon">
          <button class="button is-primary busca-btn" @click="buscar">Buscar</button>
          <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
            <Pokemon :name="poke.name" :url="poke.url" :num="index+1" />
          </div>
        </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
import Pokemon from './components/Pokemon';
export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res =>{
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  components:{
    Pokemon
  },
  computed:{
    /*resultadoBusca: function(){
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }*/
  },
  methods:{
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }
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
.busca-btn{
  margin-top: 5px;
}
</style>
