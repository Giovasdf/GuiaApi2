<script>
import axios from 'axios';
 
export default {
  data() {
    return {
      username: '',
      githubUser: null,
      pokemonName: '',
      pokemon: null,
      gender: 'male',
      randomUser: null,  
    };
  },
//   mounted() {
//   this.username = 'octocat';
//   this.buscarUsuario();
 
//   this.pokemonName = 'pikachu';
//   this.buscarPokemon();
// }
// ,
  methods: {
    async buscarUsuario() {
      try {
        const url = `https://api.github.com/users/${this.username}`;
        const { data } = await axios.get(url);
        this.githubUser = data;
      } catch (error) {
        console.error("Error al buscar usuario de GitHub", error);
        this.githubUser = null;
      }
    },
    async buscarPokemon() {
      try {
        const url = `https://pokeapi.co/api/v2/pokemon/${this.pokemonName}`;
        const { data } = await axios.get(url);
        this.pokemon = data;
      } catch (error) {
        console.error("Error al buscar Pokémon", error);
        this.pokemon = null;
      }
    },
    async buscarUsuarioPorGenero() {
      try {
        const url = `https://randomuser.me/api/?gender=${this.gender}`;
        const { data } = await axios.get(url);
        this.randomUser = data.results[0];
      } catch (error) {
        console.error("Error al buscar usuario por género", error);
        this.randomUser = null;
      }
    },
  },
};
</script>
 
<template>
  <div class="container">
    <!-- Buscador de GitHub -->
    <div class="box">
      <h2>Buscador de GitHub</h2>
      <input v-model="username" placeholder="Ingresa el nombre de usuario de GitHub" />
      <button @click="buscarUsuario">Buscar</button>
 
      <div v-if="githubUser" class="result">
        <h2>{{ githubUser.login }}</h2>
        <img :src="githubUser.avatar_url" alt="Foto de perfil" class="profile-pic" />
      </div>
    </div>
 
    <!-- Buscador de Pokémon -->
    <div class="box">
      <h2>Buscador de Pokémon</h2>
      <input v-model="pokemonName" placeholder="Ingresa el nombre o ID del Pokémon" />
      <button @click="buscarPokemon">Buscar</button>
 
      <div v-if="pokemon" class="result">
        <h2>{{ pokemon.name }} (ID: {{ pokemon.id }})</h2>
        <img :src="pokemon.sprites.front_default" alt="Imagen del Pokémon" class="pokemon-pic" />
      </div>
    </div>
 
    <!-- Buscador de usuario por género -->
    <div class="box">
      <h2>Buscador de usuario por género</h2>
      <select v-model="gender">
        <option value="male">Hombre</option>
        <option value="female">Mujer</option>
      </select>
      <button @click="buscarUsuarioPorGenero">Buscar</button>
 
      <div v-if="randomUser" class="result">
        <h2>{{ randomUser.name.first }} {{ randomUser.name.last }}</h2>
        <img :src="randomUser.picture.large" alt="Foto de perfil" class="profile-pic" />
      </div>
    </div>
  </div>
</template>
 
 
<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 50px;
}
 
/* Box*/
.box {
  background-color: #f9f9f9;
  border: 2px solid #ccc;
  padding: 20px;
  margin: 20px;
  border-radius: 10px;
  text-align: center;
  width: 300px;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
}
 
/* Input y button */
input, select {
  margin-top: 10px;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 5px;
  width: 80%;
}
 
button {
  margin-top: 15px;
  padding: 10px 20px;
  border: none;
  background-color: #5cb85c;
  color: white;
  font-size: 14px;
  border-radius: 5px;
  cursor: pointer;
}
 
button:hover {
  background-color: #4cae4c;
}
 
/* result */
.result {
  margin-top: 20px;
}
 
.profile-pic, .pokemon-pic {
  margin-top: 10px;
  width: 100px;
  height: 100px;
  border-radius: 50%;
  border: 2px solid #ddd;
  object-fit: cover;
}
</style>