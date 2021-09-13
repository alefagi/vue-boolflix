<template>
  <section id="movies">
    <h2>Movies</h2>
    <div class="flex">
      <Card v-for="movie in movies" :key="movie.id"
        :titolo="movie.title" 
        :titoloOriginale="movie.original_title"
        :lingua="movie.original_language"
        :voto="movie.vote_average" 
        :posterPath="movie.poster_path" 
        :overview="movie.overview" 
        :castName="movie.castName" />
    </div>
  </section>
</template>

<script>
import Card from './Card.vue';

export default {
  name: 'Movies',
  components: {
    Card,
  },
  props: {
    movies: Array,
  },
}
</script>

<style scoped lang="scss">
</style>