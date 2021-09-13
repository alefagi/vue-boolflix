<template>
  <div id="app">
    <header>
      <div class="container flex-between">
        <h1>BOOLFLIX</h1>
        <Search @search="getArray"/>
      </div>
    </header>
    <main> 
      <div class="container">
        <Movies :movies="movies" :movieCast="movieCast" />
        <Series :series="series" :serieCast="serieCast" />
      </div>
    </main>
  </div>
</template>

<script>
import Search from './components/Search.vue';
import Movies from './components/Movies.vue';
import Series from './components/Series.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Search,
    Movies,
    Series,
  },
  data() {
    return {
      baseUri: 'https://api.themoviedb.org/3',
      apiKey: 'f1eda9773130047c41c79c461cf79810',
      searchedText: '',
      movies: [],
      series: [],
      movieCast: [],
      serieCast: [],
    }
  },
  methods: {
    getArray(text) {
      this.searchedText = text;
      this.getMovies();
      this.getSeries();
    },
    getMovies() {
      axios
        .get(`${this.baseUri}/search/movie?api_key=${this.apiKey}&query=${this.searchedText}&language=it-IT`)
        .then((res) => {
          this.movies = res.data.results;
          // getCast
          this.movies.forEach((movie) => {
            axios
              .get(`${this.baseUri}/movie/${movie.id}?api_key=${this.apiKey}&append_to_response=credits`)
              .then((res) => {
                this.movieCast = res.data.credits.cast;
                this.movieCast.splice(5);
              });
          })
        });
    },
    getSeries() {
      axios
        .get(`${this.baseUri}/search/tv?api_key=${this.apiKey}&query=${this.searchedText}&language=it-IT`)
        .then((res) => {
          this.series = res.data.results;
          // getCast
          this.series.forEach((serie) => {
            axios
              .get(`${this.baseUri}/tv/${serie.id}?api_key=${this.apiKey}&append_to_response=credits`)
              .then((res) => {
                this.serieCast = res.data.credits.cast;
                this.serieCast.splice(5);
              });
          })
        });
    },
  },
}
</script>

<style lang="scss">
@import "./assets/scss/style.scss";
</style>
