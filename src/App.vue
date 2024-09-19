<script>
import axios from 'axios';
export default {
  data() {
    return {
      apiKey: '1d6a47b235ab92d9555727ab6c126dc7',
      searchText:'',
      movies: [],
      imgUrl: 'https://cdn.iconscout.com/icon/free/png-256/free-italy-flag-icon-download-in-svg-png-gif-file-formats--country-nation-union-flags-pack-maps-and-navigation-icons-32999.png?f=webp&w=256',
      otherImgUrl: '/vite.svg',
      anotherImgUrl: './assets/vue.svg'
    }
  },
  components: {
  },

  methods: {
    search() {
      console.log(this.searchText);
      axios
        .get('https://api.themoviedb.org/3/search/movie', {
          params: {
            api_key: this.apiKey,
            query: this.searchText,
          }
        } )
        .then((resp) => {
          console.log(resp.data);
          this.movies = resp.data.results;
        });
    },
    getFlag(lang) {
      const validLangs = [
        'en',
        'it',
        'jp'
      ];
      if(validLangs.includes(lang)) {
        if (lang == 'en') {
          return '/img_flags/en.gif';
        }
        else if (lang == 'it') {
          return '/img_flags/it.gif';
        }
        else if (lang == 'jp') {
          return '/img_flags/jp.gif';
        }
      }
      else {
        return '/img_flags/pirate.png'
      }
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
    <img src="/public/vite.svg" alt="">
    <img src="./assets/vue.svg" alt="">
    <img :src="imgUrl" alt="">
    <img :src="otherImgUrl" alt="">
    <img :src="anotherImgUrl" alt="">
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
            Lingua: <img :src="getFlag(movie.original_language)" alt="">
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
@use './style.css' as *;

img {
  max-width: 50px;
}


</style>
