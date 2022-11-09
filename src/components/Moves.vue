<template>
    <v-expansion-panels>
        <v-expansion-panel v-for="moveLearnMethod in ['level-up', 'machine', 'tutor', 'egg']" :key="moveLearnMethod">
            <v-expansion-panel-header class="text-center">{{ moveLearnMethod }}</v-expansion-panel-header>
            <v-expansion-panel-content>
                <v-simple-table>
                    <thead>
                        <tr>
                            <th class="text-left">Move</th>
                            <th class="text-left">Learn at level</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="move in moves[moveLearnMethod]" :key="move.name">
                            <td>{{ move.name | firstLetterUppercase }}</td>
                            <td>
                                <span v-show="move.level != 0">{{ move.level }}</span>
                            </td>
                        </tr>
                    </tbody>
                </v-simple-table>
            </v-expansion-panel-content>
        </v-expansion-panel>
    </v-expansion-panels>
</template>

<script>
export default {
        props:{
            selectedPokemon: Object
        },

    	methods: {
		filterMoves(pokemon) {
			return pokemon.moves.filter((item) => {
				let include = false;
				for(let version of item.version_group_details) {
					if(version.version_group.name == 'sun-moon' && version.move_learn_method.name ==  'level-up') {
						include = true;
					}
				}
				return include
			})
		},

		getMoveLevel(moveVersion) {
			for(let version of moveVersion.version_group_details) {
				if(version.version_group.name == 'sun-moon' && version.move_learn_method.name == 'level-up') {
					return version.level_learned_at
				}
			}
		}
	},

    computed: {
        moves() {
            let response = {'level-up': [], machine: [], tutor: [], egg: []};
            for (let move of this.selectedPokemon.moves) {
                for (let details of move.version_group_details) {
                    if (details.version_group.name === 'sun-moon') {
                        response[details.move_learn_method.name].push({
                            level: details.level_learned_at,
                            name: move.move.name,
                        });
                        break;
                    }
                }
            }

            for (let moveLearnMethod in response) {
                response[moveLearnMethod].sort(function (a,b) {
                    let moveA = a.level;
                    let moveB = b.level;
                    return moveA - moveB;
                })
            }
            return response;
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