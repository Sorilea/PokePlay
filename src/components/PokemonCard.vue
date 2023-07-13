
<template>
    <div>
        <h1>{{ pokemonData.name }}</h1>
        <img :src="pokemonData.sprites.front_default" alt="Pokemon Sprite" />
        <p>Types: {{ pokemonData.types.map(type => type.type.name).join(', ') }}</p>
    </div>
</template>

<script lang="ts">
import type { Pokemon } from './types';


export default {
    props: {
        pokemonData: {
            type: Object as () => Pokemon, 
            required: true
        }
    }
};
</script>
