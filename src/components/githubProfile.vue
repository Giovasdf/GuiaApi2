<script>
import axios from 'axios';

export default {
    data() {
        return {
            user: null,      
            userName: "",
            userNotFound: false 
        }
    },
    methods: {
        async getUser() {
            try {
                const url = `https://api.github.com/users/${this.userName}`;
                const { data } = await axios.get(url);
                return data;
            } catch (error) {
                return null;
            }
        },
        async setUser() {
            this.user = await this.getUser();
            if (!this.user) {
                this.userNotFound = true;   
            }
            this.userName = "";  
        }
    },
    computed: {
        userPicture() {
            // return this.user ? this.user.avatar_url : null;
            if (this.user) {
                return this.user.avatar_url;
            }
            else 
            {
                return null;
            }
        }
    }
}
</script>

<template>
    <div>
        <h1>Busca un usuario de GitHub</h1>
        <input type="text" v-model="userName">
        <button @click="setUser">Buscar</button>
        
        <div v-if="userPicture">
            <img :src="userPicture" alt="user">
            <p>¡Sí, existe!</p>
        </div>

        <div v-else-if="userNotFound">
            <p>No, no existe</p>
        </div>
        <p>------------------------------------------------------</p>
    </div>
</template>

