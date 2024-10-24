<script>
import axios from 'axios';
export default {
    data() {
        return {
            gender: '',
            user: null
        }
    },
    methods: {
        async getUser() {
            try {
                const url = `https://randomuser.me/api/?gender=${this.gender}`;
                const { data } = await axios.get(url);
                this.user = data.results;
            } catch (error) {
                console.log(error);
            }
        }
    },
    computed: {
        dataUser() {
            return {
                // name: this.user[0].name.title + ' ' + this.user[0].name.first + ' ' + this.user[0].name.last,
                name: `${this.user[0].name.title} ${this.user[0].name.first} ${this.user[0].name.last}`,
                picture: this.user[0].picture.large
            }
        }
    }
}
</script>

<template>
    <div>
        <h1>Busca un usuario por genero</h1>
        <div id="radioGroup">
            <input type="radio" id="female" value="female" v-model="gender">
            <label for="female">Female</label>
            <input type="radio" id="male" value="male" v-model="gender">
            <label for="male">Male</label>
        </div>

        <button @click="getUser">Buscar</button>

        <div v-if="user">
            <img :src="dataUser.picture" >
            <h3>{{ dataUser.name }}</h3>
        </div>
    </div>
</template>
