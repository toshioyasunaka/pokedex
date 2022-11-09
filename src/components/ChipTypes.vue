<template>
    <div>
        <v-chip label                                 
            v-for="(type, index) in selectedPokemon.types" :key="index"
            class="mr-1"
            :style="'backgroundColor:' + getColor(type.type.name)"
            >
            {{ type.type.name | firstLetterUppercase}}
        </v-chip>
    </div>
</template>

<script>
export default {
    props: {
        selectedPokemon: Object
    },

    filters: {
        firstLetterUppercase(name) {
            // return name.split("")[0].toUpperCase() + name.slice(1)
            return name.charAt(0).toUpperCase() + name.slice(1)
        },
    },

    methods: {
        getColor(type) {
            switch(type) {
                case 'normal': return '#A9A982';
                case 'fighting': return '#B63228';
                case 'flying': return '#A995DE';
                case 'poison': return '#8A3272';
                case 'ground': return '#D8C380';
                case 'rock': return '#B79D3B';
                case 'bug': return '#A9B61B';
                case 'ghost': return '#745891';
                case 'steel': return '#B7B5D1';
                case 'fire': return '#F77A32';
                case 'water': return '#6A91E6';
                case 'grass': return '#68C952';
                case 'electric': return '#DBC14A';
                case 'psychic': return '#F3628C';
                case 'ice': return '#99D7DA';
                case 'bug': return '#A8B622';
                case 'dragon': return '#703EFA';
                case 'dark': return '#725947';
                case 'fairy': return '#E2A5E3';
                case 'unknown': return 'A9A982';
                case 'shadow': return '#745646';
                default: return 'red';
            }
        }
    }
}
</script>

<style>

</style>