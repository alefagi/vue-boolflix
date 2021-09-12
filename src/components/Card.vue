<template>
  <div>
    <ul>
      <li>Titolo: {{ titolo }}</li>
      <li>Titolo Originale: {{ titoloOriginale }} </li>
      <li>Lingua: 
        <img v-if="!imgNotFound" :src="getLanguageFlag(lingua)" :alt="lingua">
        <span v-else>{{ lingua }}</span>
      </li>
      <li>Voto: {{ voto }}</li>
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
  },
  data() {
    return {
      imgNotFound: false,
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
}
</script>

<style scoped lang="scss">
img {
  width: 30px;
}

</style>