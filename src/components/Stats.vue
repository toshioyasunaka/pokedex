<template>
  <div class="d-flex justify-space-around mb-5">
    <v-chip
      v-for="stat in stats" :key="stat.name"
      :class="getColor(stat.stat.name)"
      label
    >
      {{ stat.stat.name | firstLetterUppercase }} | {{ stat.base_stat }}
    </v-chip>
  </div>
</template>

<script>
export default {
  props: {
    stats: Array
  },

  methods: {
    getColor(statName) {
      switch(statName) {
        case 'hp': return 'red lighten-1';
        case 'attack': return 'orange lighten-1';
        case 'defense': return 'yellow lighten-1';
        case 'special-attack': return 'blue lighten-1';
        case 'special-defense': return 'light-green lighten-1';
        case 'speed': return 'purple lighten-1';
        default: return 'gray'
      }
    }
  },

  filters: {
    firstLetterUppercase(name) {
      // return name.split("")[0].toUpperCase() + name.slice(1)
      return name.charAt(0).toUpperCase() + name.slice(1)
    },
	}
}
</script>

<style>

</style>