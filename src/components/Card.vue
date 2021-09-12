<template>
  <div class="card">
    <ul>
      <li>Titolo: {{ titolo }}</li>
      <li>Titolo Originale: {{ titoloOriginale }} </li>
      <li>Lingua: 
        <img v-if="!imgNotFound" :src="getLanguageFlag(lingua)" :alt="lingua">
        <span v-else>{{ lingua }}</span>
      </li>
      <li>Voto: {{ voteToInteger }}</li>
      <li><img :src="`${posterUri}${posterPath}`" :alt="titolo"></li>
    </ul>
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
img {
  width: 30px;
}

.card {
  width: 300px;
  height: 200px;
}

</style>