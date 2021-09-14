<template>
  <div class="card">
    <div class="card-layover">
      <img v-if="posterPath" :src="`${posterUri}${posterPath}`" :alt="titolo">
      <img v-else class="not-found" src="@/assets/images/no-image.jpg" alt="no-image">
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
          <i v-for="n in 5" :key="n" :class="n <= voteToInteger ? 'fas':'far'" class="fa-star"></i>
        </li>
        <li><span>Overview: </span>{{ overview }}</li>
        <li><span>Genere: </span>{{ genreName }}</li>
        <li><span>Attori: </span>{{ actorName }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Card',
  props: {
    titolo: String,
    titoloOriginale: String,
    lingua: String,
    voto: Number,
    posterPath: String,
    overview: String,
    id: Number, 
    kind: String,             
  },
  data() {
    return {
      baseUri: 'https://api.themoviedb.org/3',
      apiKey: 'f1eda9773130047c41c79c461cf79810',
      imgNotFound: false,
      posterUri: 'http://image.tmdb.org/t/p/w342',
      actorName: '',
      genreName: '',
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
  },
  mounted() {
    if (this.kind === 'movie') {
      axios
        .get(`${this.baseUri}/movie/${this.id}?api_key=${this.apiKey}&append_to_response=credits`)
        .then((res) => {
          const actors = res.data.credits.cast.splice(0, 5);
          this.actorName = actors.map((actor) => {
            return actor.name;
          })
          this.actorName = this.actorName.join(', ');
        });
      axios
        .get(`${this.baseUri}/movie/${this.id}?api_key=${this.apiKey}&append_to_response=credits`)
        .then((res) => {
          const genres = res.data.genres;
          this.genreName = genres.map((genre) => {
            return genre.name;
          })
          this.genreName = this.genreName.join(', ');
        })
    }
    else if (this.kind === 'serie') {
      axios
        .get(`${this.baseUri}/tv/${this.id}?api_key=${this.apiKey}&append_to_response=credits`)
        .then((res) => {
          const actors = res.data.credits.cast.splice(0, 5);
          this.actorName = actors.map((actor) => {
            return actor.name;
          })
          this.actorName = this.actorName.join(', ');
        });
      axios
        .get(`${this.baseUri}/tv/${this.id}?api_key=${this.apiKey}&append_to_response=credits`)
        .then((res) => {
          const genres = res.data.genres;
          this.genreName = genres.map((genre) => {
            return genre.name;
          })
          this.genreName = this.genreName.join(', ');
        })
    }
  }
}
</script>

<style scoped lang="scss">
</style>