<template>
    <div>
        <h1>{{ pokemonData?.name }}</h1>
        <template v-if="pokemonData && pokemonData.sprites && pokemonData.sprites.front_default">
            <img :src="pokemonData.sprites.front_default" alt="Pokemon Sprite" />
        </template>
        <p v-else>Loading...</p>
    </div>
</template>

<script lang="ts">
import axios from 'axios';

interface Pokemon {
    name: string;
    sprites: {
        front_default: string;
    };
}

export default {
    data() {
        return {
            pokemonData: null as Pokemon | null
        };
    },
    mounted() {
        this.fetchPokemonData();
    },
    methods: {
        fetchPokemonData() {
            axios
                .get('https://pokeapi.co/api/v2/pokemon/1')
                .then(response => {
                    this.pokemonData = response.data as Pokemon;
                })
                .catch(error => {
                    console.error(error);
                });
        }
    }
};
</script>
