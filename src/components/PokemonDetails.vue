<template>
	<v-dialog
		width="800"
		v-if="selectedPokemon"
		v-model="activeDialog"
		>
		<v-card>
			<v-container>
				<v-row class="d-flex align-center">
					<v-col cols="4">
						<v-img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${(selectedPokemon.id)}.png`"
							:alt="`Sprite ${selectedPokemon.name}`" 
							width="100%"
						/>
					</v-col>
					<v-col cols="8">
						<h1>{{ selectedPokemon.name | firstLetterUppercase }}</h1>
						<ChipTypes :selectedPokemon="selectedPokemon"/>
						<v-divider class="my-2"></v-divider>
						<v-chip label>
							Altura {{ selectedPokemon.height * 0.10 | height }}m
						</v-chip>
						<v-chip label class="ml-2">
							Peso {{ (selectedPokemon.weight * 0.10).toFixed(1) }}kg
						</v-chip>
					</v-col>
				</v-row>    

				<div class="mb-3 ml-1">
					<h2 class="d-inline-flex">Status</h2>
				</div>
				<Stats :stats="selectedPokemon.stats"/>

				<div class="mb-3 ml-1">
					<h2 class="d-inline-flex">Moves</h2>
					<v-badge		
					class="ml-2"				
						content="i"
						title="Based on the game Sun and Moon"
					></v-badge>
				</div>
				<Moves :selectedPokemon="selectedPokemon"/>

				<div class="mb-3 ml-1 mt-5">
					<h2 class="d-inline-flex">Evolution</h2>
				</div>
				<EvolutionaryLine :selectedPokemon="selectedPokemon"/>
			</v-container>
		</v-card>
	</v-dialog>
</template>

<script>
import ChipTypes from './ChipTypes'
import Moves from './Moves'
import Stats from './Stats'
import EvolutionaryLine from './EvolutionaryLine'

export default {
	components: {ChipTypes, Moves, Stats, EvolutionaryLine},

	props: {
		selectedPokemon: Object,
		showDialog: Boolean
	},

	filters: {
		firstLetterUppercase(name) {
			// return name.split("")[0].toUpperCase() + name.slice(1)
			return name.charAt(0).toUpperCase() + name.slice(1)
		},

		height(height) {
			return height.toFixed(2)
		}
	},
	
	computed: {
		activeDialog: {
			get: function() {
				return this.showDialog
			},
			set: function() {
				this.$emit('closeDialog', this.showDialog)
			}
		}
	}
}
</script>

<style>

</style>