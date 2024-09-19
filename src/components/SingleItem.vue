<script>
export default {
  data() {
    return {
      baseImgUrl: 'https://image.tmdb.org/t/p/',
      posterSize: 'w342'
    };
  },
    props: {
        title: String,
        originalTitle: String,
        language: String,
        vote: Number,
        posterPath: String,
    },
    methods: {
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
    <ul>
      <li>
        <img :src="baseImgUrl + posterSize + posterPath" alt="">
      </li>
          <li>
            Titolo: {{ title }}
          </li>
          <li>
            Titolo originale: {{ original_title }}
          </li>
          <li>
            Lingua: <img :src="getFlag(language)" alt="">
          </li>
          <li>
            Voto: {{ vote }}
          </li>
        </ul>
</template>

<style scoped>
</style>