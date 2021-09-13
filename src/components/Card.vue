<template>
  <div class="card">
    <div class="card-layover">
      <img v-if="posterPath" :src="`${posterUri}${posterPath}`" :alt="titolo">
    </div>
    <div class="card-text">
      <ul>
        <li><span>Titolo: </span>{{ titolo }}</li>
        <li><span>Titolo Originale: </span>{{ titoloOriginale }} </li>
        <li><span>Lingua: </span>
          <img class="lang" v-if="!imgNotFound" :src="getLanguageFlag(lingua)" :alt="lingua">
          <span v-else>{{ lingua }}</span>
        </li>
        <li>
          <span>Voto: </span>
          <i v-for="n in voteToInteger" :key="n" class="fas fa-star"></i>
          <i v-for="n in 5-voteToInteger" :key="n" class="far fa-star"></i>
        </li>
        <li><span>Overview: </span>{{ overview }}</li>
        <!-- <li><span>Attori: </span>{{ castName }}</li> -->
      </ul>
      <img class="not-found" v-if="!posterPath" src="@/assets/images/no-image.jpg" alt="no-image">  
    </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    titolo: String,
    titoloOriginale: String,
    lingua: String,
    voto: Number,
    posterPath: String,
    overview: String,
    castName: String,
  },
  data() {
    return {
      imgNotFound: false,
      posterUri: 'http://image.tmdb.org/t/p/w342',
    }
  },
  methods: {
    getLanguageFlag(lingua) {
      switch (lingua) {
        case 'it':
          return lingua = require ('@/assets/images/it.png');
        case 'en':
          return lingua = require ('@/assets/images/en.png');
        default:
          this.imgNotFound = true;
          return lingua;
      }
    },
  },
  computed: {
    voteToInteger() {
      let voteInt = Math.ceil(this.voto / 2);
      return voteInt;
    }
  }
}
</script>

<style scoped lang="scss">
</style>