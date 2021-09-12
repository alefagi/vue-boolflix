<template>
  <section id="series">
    <h2>TV Series</h2>
    <div class="flex">
      <Card v-for="(serie, id) in series" :key="id" :titolo="serie.name" :titoloOriginale="serie.original_name" :lingua="serie.original_language" :voto="serie.vote_average" :posterPath="serie.poster_path"/>
    </div>
  </section>
</template>

<script>
import Card from './Card.vue';


export default {
  name: 'Series',
  components: {
    Card,
  },
  props: {
    series: Array,
  },
}
</script>

<style scoped lang="scss">
</style>