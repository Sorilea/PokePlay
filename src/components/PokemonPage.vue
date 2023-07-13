<template>
    <div>
        <h1>Pokémon Page</h1>
        
        <ul v-if="pokemonData">
            <li v-for="pokemon in pokemonData">
                <PokemonCard :pokemonData="pokemon" v-if="pokemonData" />
            </li>
        </ul>

        <p v-else>Loading...</p>
    </div>
</template>

<script lang="ts">
import axios from 'axios';
import {type Pokemon} from './types'
import PokemonCard from './PokemonCard.vue';


export default {
    components: {
        PokemonCard
    },
    data() {
        return {
            pokemonData: null as Pokemon[] | null
        };
    },
    mounted() {
        this.fetchPokemonData();
    },
    methods: {
        fetchPokemonData() {
            axios
                .get('https://pokeapi.co/api/v2/pokemon/')
                .then(response => {
                    this.pokemonData = response.data.results.map((pokemon: any) => {
                        return {
                            id: pokemon.id,
                            name: pokemon.name,
                            sprites: {}, // Add sprite data if needed
                            types: [] // Add type data if needed
                        };
                    });
                })
                .catch(error => {
                    console.error(error);
                });
        }
    }
};
</script>
