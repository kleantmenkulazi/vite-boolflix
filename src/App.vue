<script>
import axios from 'axios';
export default {
  data() {
    return {
      apiKey: '1d6a47b235ab92d9555727ab6c126dc7',
      searchText:'',
      movies: []
    }
  },
  components: {
  },

  methods: {
    search() {
      console.log(this.searchText);
      axios
        .get('https://api.themoviedb.org/3/search/movie',{
          params: {
            api_key: this.apiKey,
            query: this.searchText,
          }
        } )
        .then((resp) => {
          console.log(resp.data);
        });
    }
    }
  }

</script>

<template>
  <div>
    <div>
      <form @submit.prevent="search">
        <input v-model="searchText" type="text" placeholder="Cerca info...">
        <button type="submit">
          Cerca
        </button>
      </form>
    </div>
    <div>
      <input v-model="searchText" type="text" placeholder="Cerca info...">
      <button @click="search">
        Cerca
      </button>
    </div>
  </div>
  <div>
    <ol>
      <li v-for="(movie, i) in movie" :key="i">
        <ul>
          <li>
            Titolo: {{ movie.title }}
          </li>
          <li>
            Titolo originale: {{ movie.original_title }}
          </li>
          <li>
            Lingua: {{ movie.original_language }}
          </li>
          <li>
            Voto: {{ movie.vote_avarage }}
          </li>
        </ul>
        <hr>
      </li>
    </ol>
  </div>
  
</template>

<style lang="scss">
@use 'assets/scss/main' as *;

@import 'bootstrap/scss/bootstrap';
</style>
