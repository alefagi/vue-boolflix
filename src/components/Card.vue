<template>
  <div>
    <ul>
      <li>Titolo: {{ titolo }}</li>
      <li>Titolo Originale: {{ titoloOriginale }} </li>
      <li>Lingua: {{ lingua }}</li>
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
  }
}
</script>

<style scoped lang="scss">

</style>