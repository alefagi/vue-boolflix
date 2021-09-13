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
        this.getMovies('/search/movie', '/movie/');
        this.getSeries('/search/tv', '/tv/');
      }
    },
    getCast(item, cast) {
      let castName = [];
      cast.forEach((actor) => {
        castName.push(actor.name);
        item.castName = castName.join(', ');
      });
    },
    getGenre(item, genre) {
      let genreName = [];
      genre.forEach((genre) => {
        genreName.push(genre.name);
        item.genreName = genreName.join(', ');
      });
    },
    getMovies(searchEP, creditsEP) {
      axios
        .get(`${this.baseUri}${searchEP}?api_key=${this.apiKey}&query=${this.searchedText}&language=it-IT`)
        .then((res) => {
          const temp = res.data.results;
          // getDetails
          temp.forEach((item) => {
            axios
              .get(`${this.baseUri}${creditsEP}${item.id}?api_key=${this.apiKey}&append_to_response=credits`)
              .then((res) => {
                //getCast
                const cast = res.data.credits.cast.splice(0, 5);
                this.getCast(item, cast);
                //getGenre
                const genre = res.data.genres;
                this.getGenre(item, genre);
              })
            setTimeout(() => { this.movies = temp }, 500);
          });
        });
    },
    getSeries(searchEP, creditsEP) {
      axios
        .get(`${this.baseUri}${searchEP}?api_key=${this.apiKey}&query=${this.searchedText}&language=it-IT`)
        .then((res) => {
          const temp = res.data.results;
          // getDetails
          temp.forEach((item) => {
            axios
              .get(`${this.baseUri}${creditsEP}${item.id}?api_key=${this.apiKey}&append_to_response=credits`)
              .then((res) => {
                //getCast
                const cast = res.data.credits.cast.splice(0, 5);
                this.getCast(item, cast);
                //getGenre
                const genre = res.data.genres;
                this.getGenre(item, genre);
              })
            setTimeout(() => { this.series = temp }, 500);
          });
        });
    },
  },
}
</script>

<style lang="scss">
@import "./assets/scss/style.scss";
</style>
