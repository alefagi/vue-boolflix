<template>
  <div id="app">
    <header>
      <div class="container flex-center">
        <h1>BOOLFLIX</h1>
        <Search @search="getArray"/>
      </div>
    </header>
    <main> 
      <div class="container">
        <Movies :movies="movies" />
        <Series :series="series" />
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
        });
    },
    getSeries() {
      axios
        .get(`${this.baseUri}/search/tv?api_key=${this.apiKey}&query=${this.searchedText}&language=it-IT`)
        .then((res) => {
          this.series = res.data.results;
        });
    },
  },
}
</script>

<style lang="scss">
@import "./assets/scss/style.scss";

header {
  background-color: #000;
  height: 100px;
  h1 {
    color: red;
  }
};

main {
  background-color: grey;
}
</style>
