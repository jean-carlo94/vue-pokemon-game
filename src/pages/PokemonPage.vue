<template>
    <h1 v-if="!pokemon" class="fade-in">Espere por favor...</h1>

    <div v-else class="container fade-in">
        <h1>¿ Quien es este Pokemon ?</h1>
        <PokemonPicture 
            :pokemonId="pokemon.id" 
            :showPokemon="showPokemon"
        />
        <PokemonOptions 
            :pokemonsOptions="pokemonArr" 
            @selectionPokemon="checkAnswer"
        />
    </div>

    <template v-if=" message !== '' ">
        <h2>{{ message }}</h2>
        <button @click="newGame"> Nuevo Juego </button>
    </template>
</template>

<script>
    import PokemonPicture from '../components/PokemonPicture.vue';
    import PokemonOptions from '../components/PokemonOptions.vue';
    import getPokemonOptions from '../helpers/getPokemonOptions';

    export default {
        components: { PokemonOptions, PokemonPicture },
        data() {
            return {
                pokemonArr: [],
                pokemon: null,
                showPokemon: false,
                message: '',
            }
        },
        methods: {
            async mixPokemonArray() {
                this.pokemonArr = await getPokemonOptions();

                const randomInt = Math.floor( Math.random() * 4 );
                this.pokemon = this.pokemonArr[randomInt]
            },
            checkAnswer( pokemonId ) {
                this.showPokemon = true;
                this.message = this.pokemon.id === pokemonId ? `Correcto!!, ${this.pokemon.name}` : `Oops!!, era ${this.pokemon.name}`;
            },
            newGame(){
                this.showPokemon = false
                this.message = '';
                this.pokemonArr = [];
                this.pokemon = null;
                this.mixPokemonArray();
            }
        },
        mounted() {
            this.mixPokemonArray()
        },
    }
</script>

<style scoped>

</style>