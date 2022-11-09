<template>
  <v-container>
    <v-text-field
      label="Pesquisar"
      placeholder="Ex: Bulbasaur"
      solo
      v-model="search"
    ></v-text-field>

    <v-row>
      <v-col cols=2 sm="6" md="4" lg="2" v-for="pokemon in filteredPokemons" :key="pokemon.name">
        <PokemonCard :pokemon="pokemon"/>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import PokemonCard from './PokemonCard'

export default {
  components: {
    PokemonCard
  },

  props: {
    pokemons: Array
  },

  data() {
    return {
      search: "",
    }
  },

  computed: {
    filteredPokemons() {
      return this.pokemons.filter((pokemon) => {
        return pokemon.name.includes(this.search.trim().toLowerCase())
      })
    }
  },
}
</script>

<style>

</style>