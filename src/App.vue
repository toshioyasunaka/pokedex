<template>
  <v-app>
    <v-container>
      <v-container>
        <v-row>
          <v-container>
            <v-img
              contain
              height="300"
              src="https://www.nicepng.com/png/full/228-2285786_pokedex-kanto-pokedex-de-kanto.png"
              class="d-flex text-center"
              style="transform: rotate(-22deg)"
            ></v-img>
            <h1 
            class="white--text text-center"
            style="font-size:6rem">
              Pokedex
            </h1>
          </v-container>
        </v-row>

        <PokemonsGrid :pokemons='pokemons'/>
      </v-container>
    </v-container>
  </v-app>
</template>

<script>
import PokemonsGrid from './components/PokemonsGrid.vue'
import axios from 'axios'

export default {
  name: 'App',

  components: {
    PokemonsGrid
  },

  data() {
    return {
      pokemons: []
    }
  },
  
  mounted() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151')
      .then((response) => {
        this.pokemons = response.data.results
      })
  }
}
</script>

<style>
  #app {
    background: linear-gradient(
        to bottom right,
        rgba(10, 10, 10, 1),
        rgba(12, 39, 63, 1)
      )
      no-repeat center center fixed !important;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover !important;
    background-position: center;
    min-height: 100vh;
  }
</style>