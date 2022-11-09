<template>
  <div>
    <v-row class="d-flex justify-center align-center">
        <template v-for="(evolution_detail, index) in evolutions()">
            <v-col cols="12" md="3" :key="`evolution-${index}`"
            v-if="getEvolutionDetailsLength(evolution_detail) == 2"
            class="d-flex justify-center text-center">
                <div class="d-flex flex-column">
                    <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${getId(evolution_detail)}.png`" alt="Pokemon Image">
                    <h3>{{ evolution_detail.name | firstLetterUppercase }}</h3>
                </div>
            </v-col>

            <v-col md="1" :key="`evolution-${index}`" v-else
            class="d-flex flex-column justify-center text-center">
                <h4>{{ evolution_detail.trigger.name | triggerName }}</h4>
                <h4 class="text-center">{{ evolution_detail.min_level }}</h4>
            </v-col>
        </template>
    </v-row>
  </div>
</template>

<script>
import axios from 'axios'

export default {
    props: {
        selectedPokemon: Object,
    },

    data() {
        return {
            evolution: null
        }
    },

    mounted() {
        this.fecthEvolution()
    },

    methods: {
        fecthEvolution() {
            axios
                .get(`https://pokeapi.co/api/v2/pokemon-species/${this.selectedPokemon.id}`)
                .then((response) => {
                    axios.get(response.data.evolution_chain.url)
                        .then((response) => {
                            this.evolution = response.data.chain;
                        })
                })
        },

        evolutions() {
            let chain = [];
            let evolution = this.evolution;

            if(evolution.species) {
                chain.push(evolution.species)
            }

            while(evolution.species) {
                if(evolution.evolves_to.length) {
                    evolution = evolution.evolves_to[0]

                    if(evolution.evolution_details && 
                    evolution.evolution_details[0].min_level
                    ){
                        chain.push(evolution.evolution_details[0]);
                    }

                    if(evolution.species) {
                        chain.push(evolution.species);
                    }
                } else {
                    break;
                }
            }
            return chain;
        },

        getId(details) {
            let id = details.url.split("/")[6]
            return id
        },

        getEvolutionDetailsLength(details) {
            let detailsLength = Object.keys(details).length
            return detailsLength
        },
    }, 

    filters: {
        firstLetterUppercase(name) {
            return name.charAt(0).toUpperCase() + name.slice(1);
        },

        triggerName(name) {
            let modifiedName;
            if (name === "level-up") {
                modifiedName =  name.split("-")[0]
                return modifiedName.charAt(0).toUpperCase() + modifiedName.slice(1)
            }
        }
    }
}
</script>


