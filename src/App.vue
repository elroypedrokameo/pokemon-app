<template>
  <div class="container">
    <h1>Pokemon's</h1>
    <PokemonList :apiUrl="apiUrl" :imageUrl="imageUrl" />
  </div>
</template>

<script>
  import PokemonList from './views/PokemonList.vue'

  export default {
    data: () => {
      return {
        imageUrl: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
        apiUrl: 'https://pokeapi.co/api/v2/pokemon/'
      }
    },
    components: {
      PokemonList
    }
  }
</script>

<style scoped>
  .container {
    display: flex;
    justify-content: center;
    margin-left: 250px;
    align-items: center;
    flex-direction: column;
    padding: 10px;
    /* width: 400px; */
    width: calc(100% - 20px);
    min-height: calc(100vh - 20px);
    background: radial-gradient(#156F99, #0A2E50);
    font-family: 'Acme', arial;
    font-size: 1rem;
    font-weight: normal;
  }

  h1 {
    color: #efefef;
    padding: 50px;
  }
</style>
