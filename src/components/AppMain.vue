<script>
  import { store } from '../store.js';
  import SingleItem from './SingleItem.vue';
  // my-component.js
export default {
  data() {
    return {
      store
    };
  },
  methods: {
    
  },

  components: {
    AppHeader,
    SingleItem,
  },
}
</script>

<template>
  <div>
    <h2>
      Movies
    </h2>
    <ol>
      <li v-for="(movie, i) in store.movie" :key="i">
        <SingleItem
        :title="movie.title"
        :originalTitle="movie.originalTitle"
        :language="movie.original_language"
        :vote="movie.vote_avarage"
        :posterPath="movie.posterPath"
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
      <li v-for="(serie, i) in store.series" :key="i">

        <SingleItem
        :title="serie.name"
        :originalTitle="serie.original_name"
        :language="serie.original_language"
        :vote="serie.vote_avarage"
        :posterPath="serie.posterPath"
        />
        
        <hr>
      </li>
    </ol>
  </div>
</template>

<style scoped>

</style>
