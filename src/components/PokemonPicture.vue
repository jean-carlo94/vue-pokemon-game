<template>
    <h3>Pokemon Picture</h3>
    <div class="pokemon-container">
        <img v-if="!showPokemon" class="hidden-pokemon" :src="imgSrc" alt="Pokemon">
        <img v-else class="fade-in" :src="imgSrc" alt="Pokemon">
    </div>
</template>

<script >
export default {
    props: {
        pokemonId: {
            type: Number,
            required: true,
            validator( value ){
                return value > 0
            }
        },
        showPokemon: {
            type:  Boolean,
            required: true,
            default: false,
        },
    },
    computed: {
        imgSrc() {
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`
        }
    }
}
</script>

<style scoped>
    /* Pokemon Picture */

img {
    height: 200px;
    user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -webkit-user-drag: none;
    -webkit-user-select: none;
}
.hidden-pokemon {
    filter: brightness(0);
}
.pokemon-container {
    height: 200px;
}

</style>