<template>
	<v-card @click="showPokemon(getId(pokemon))" :flat="flat">
		<v-container>
			<v-row class="mx-0 d-flex flex-column align-center">   
				<v-img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${(getId(pokemon))}.png`"
					:alt="`Sprite ${pokemon.name}`" 
					width="80%"
				/>
				<h2 class="text-center">
					{{ pokemon.name | firstLetterUppercase }}
				</h2>
			</v-row>    
		</v-container>
		<PokemonDetails @closeDialog="showDialog = $event" :showDialog="showDialog" :selectedPokemon="selectedPokemon"/>
	</v-card>
</template>

<script>
import axios from 'axios'
import PokemonDetails from './PokemonDetails.vue'

export default {
	components: {PokemonDetails},

	props: {
		pokemon: Object,
		flat: {
			type: Boolean,
			default: false,
		},
	},

	data() {
		return {
			showDialog: false,
			selectedPokemon: null,
		}
	},

	methods: {
		getId(pokemon) {
			return Number(pokemon.url.split("/")[6])
		},
			
		showPokemon(id) {
			axios
				.get(`https://pokeapi.co/api/v2/pokemon/${id}`)
				.then((response) => {
				this.selectedPokemon = response.data
				this.showDialog = !this.showDialog
			})
		},
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