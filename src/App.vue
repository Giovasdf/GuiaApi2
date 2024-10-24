<script>
import githubProfile from './components/githubProfile.vue';
import pokemon from './components/pokemon.vue';
import randomUser from './components/randomUser.vue';
export default {
  components: {
    githubProfile,
    pokemon,
    randomUser
  }
}

</script>

<template>
  <div>
    <githubProfile/>
    <pokemon/>
    <randomUser/>
  </div>
</template>

<style scoped>
</style>
