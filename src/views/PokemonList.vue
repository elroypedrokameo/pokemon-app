<template>
  <div class="list">
    <article class="card-pokemon" v-for="(pokemon, index) in pokemons" :key="'poke'+index">
      <img class="pokemon-img" :src="imageUrl + pokemon.id + '.png'" width="96" height="96" alt="pokemonimg">
      <h3 class="pokemon-name">{{ pokemon.id }} - {{ pokemon.name }}</h3>
    </article>
    <div id="scroll-trigger" ref="infinitescrolltrigger">

    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  props: [
    'apiUrl',
    'imageUrl'
  ],
  data: () => {
    return {
      pokemons: [],
      nextUrl: ''
    }
  },
  methods: {
    async fetchData() {
      try {
        let response = await axios.get(this.apiUrl)
        let poke = response.data.results
        poke.forEach(pokemon => {
          pokemon.id = pokemon.url.split('/')
            .filter(function(part) { return !!part }).pop()
          this.pokemons.push(pokemon)
        });
      } catch (err) {
        console.log('Gagal fetch data', err)
      }
    }
  },
  created() {
    this.fetchData();
  }
}
</script>

<style scoped>
  .list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    grid-gap: 10px;
    width: 100%;
    max-width: 510px;

  }

  .card-pokemon {
    height: 150px;
    background-color: #efefef;
    text-align: center;
    text-transform: capitalize;
    border-radius: 5px;
    cursor: pointer;
    box-shadow: 0 15px 30px rgba(0, 0, 0, .2), 
                0 10px 10px rgba(0, 0, 0, .2);
  }

  .pokemon-img {
    transition: .2s;
  }
  .pokemon-img:hover {
    transform: scale(1.2);
  }

  .pokemon-name {
    margin: 0;
  }
</style>