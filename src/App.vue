<script>
import axios from 'axios';
import { store } from './components/store.js';

import AppHeader from './AppHeader.vue';
import SingleItem from './components/SingleItem.vue';
import AppHeader from './AppHeader.vue';
export default {
  data() {
    return {
      store,
      apiKey: '1d6a47b235ab92d9555727ab6c126dc7',
      movies: [],
      series: [],
      imgUrl: 'https://cdn.iconscout.com/icon/free/png-256/free-italy-flag-icon-download-in-svg-png-gif-file-formats--country-nation-union-flags-pack-maps-and-navigation-icons-32999.png?f=webp&w=256',
      otherImgUrl: '/vite.svg',
      anotherImgUrl: './assets/vue.svg'
    }
  },
  components: {
    AppHeader,
    SingleItem,
  },

  methods: {
    search() {
      console.log(this.store.searchText);

      axios
        .get('https://api.themoviedb.org/3/search/movie', {
          params: {
            api_key: this.apiKey,
            query: this.store.searchText,
          }
        } )
        .then((resp) => {
          console.log('Movies',resp.data);
          this.movies = resp.data.results;
        });

        axios
        .get('https://api.themoviedb.org/3/search/tv', {
          params: {
            api_key: this.apiKey,
            query: this.store.searchText,
          }
        } )
        .then((resp) => {
          console.log('Series',resp.data);
          this.series = resp.data.results;
        });
    },
    getFlag(lang) {
      const validLangs = [
        'en',
        'it',
        'ja'
      ];
      if(validLangs.includes(lang)) {
        if (lang == 'ja') {
          return '/img_flags/jp.gif';
        }
        else {
          return '/img_flags/' + lang + '.gif';
        }
      }
      else {
        return '/img_flags/pirate.png';
      }
    }

    }
  }

</script>

<template>
  
  
  <AppHeader @search="search()"/>
  
  <div>
    <h2>
      Movies
    </h2>
    <ol>
      <li v-for="(movie, i) in movie" :key="i">
        <SingleItem
        :title="movie.title"
        :originalTitle="movie.originalTitle"
        :language="movie.original_language"
        :vote="movie.vote_avarage"
        />
        
        <hr>
      </li>
    </ol>
  </div>

  <hr>

  <div>
    <h2>
      Series
    </h2>
    <ol>
      <li v-for="(serie, i) in series" :key="i">

        <SingleItem
        :title="serie.name"
        :originalTitle="serie.original_name"
        :language="serie.original_language"
        :vote="serie.vote_avarage"
        />
        
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
