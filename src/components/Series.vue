<template>
  <section id="series">
    <h2>TV Series</h2>
    <div class="flex">
      <Card v-for="serie in series" :key="serie.id" 
        :titolo="serie.name" 
        :titoloOriginale="serie.original_name" 
        :lingua="serie.original_language" 
        :voto="serie.vote_average" 
        :posterPath="serie.poster_path" 
        :overview="serie.overview" 
        :castName="serie.castName"/>
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