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
      if (text.length) {
        this.searchedText = text;
        this.getMovies();
        this.getSeries();
      }
    },
    getMovies() {
      axios
        .get(`${this.baseUri}/search/movie?api_key=${this.apiKey}&query=${this.searchedText}&language=it-IT`)
        .then((res) => {
          this.tempMovies = res.data.results;
          // getDetails
          this.tempMovies.forEach((movie) => {
            axios
              .get(`${this.baseUri}/movie/${movie.id}?api_key=${this.apiKey}&append_to_response=credits`)
              .then((res) => {
                //getCast
                const movieCast = res.data.credits.cast.splice(0, 5);
                let castName = [];
                movieCast.forEach((actor) => {
                  castName.push(actor.name);
                  movie.castName = castName.join(', ');
                });
                //getGenre
                const movieGenre = res.data.genres;
                let genreName = [];
                movieGenre.forEach((genre) => {
                  genreName.push(genre.name);
                  movie.genreName = genreName.join(', ');
                });
              })
            setTimeout(() => { this.movies = this.tempMovies }, 500);
          });
        });
    },
    getSeries() {
      axios
        .get(`${this.baseUri}/search/tv?api_key=${this.apiKey}&query=${this.searchedText}&language=it-IT`)
        .then((res) => {
          this.tempSeries = res.data.results;
          // getDetails
          this.tempSeries.forEach((serie) => {
            axios
              .get(`${this.baseUri}/tv/${serie.id}?api_key=${this.apiKey}&append_to_response=credits`)
              .then((res) => {
                //getCast
                const serieCast = res.data.credits.cast.splice(0, 5);
                let castName = [];
                serieCast.forEach((actor) => {
                  castName.push(actor.name);
                  serie.castName = castName.join(', ');
                });
                //getGenre
                const serieGenre = res.data.genres;
                let genreName = [];
                serieGenre.forEach((genre) => {
                  genreName.push(genre.name);
                  serie.genreName = genreName.join(', ');
                });
              })
            setTimeout(() => { this.series = this.tempSeries }, 500);
          });
        });
    },
  },
}
</script>

<style lang="scss">
@import "./assets/scss/style.scss";
</style>
