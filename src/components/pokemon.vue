<script>
import axios from 'axios';

export default {
    data() {
        return {
            pokemonSearch: '',  
            pokemon: null,      
        }
    },
    methods: {
        async getPokemon() {
            try {
                const url = `https://pokeapi.co/api/v2/pokemon/${this.pokemonSearch.toLowerCase()}`
                const { data } = await axios.get(url)
                this.pokemon = data
            } catch (error) {
                this.pokemon = null
            }
        }
    },
    computed: {
        pokemonData() {
            if (!this.pokemon) {
                return null
            }
            return {
                name: this.pokemon.name,
                img: this.pokemon.sprites?.other?.dream_world?.front_default || this.pokemon.sprites?.front_default
            };
        }
    }
}
</script>

<template>
    <div>
        <h1>Busca tu Pokémon</h1>
        <h2>Usa un número o el nombre del Pokémon</h2>

        <input type="text" v-model="pokemonSearch" >
        <button @click="getPokemon">Buscar</button>


        <div v-if="pokemonData">
            <img :src="pokemonData.img" alt="Imagen del Pokémon">
            <h3>{{ pokemonData.name }}</h3>
        </div>
        <p>------------------------------------------------------</p>

    </div>
</template>
