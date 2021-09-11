<template>
  <div id="app">
    <header>
      <div class="container flex-between">
        <h1>BOOLFLIX</h1>
        <Search />
      </div>
    </header>
    <main> 
      <div class="container">
        <section id="movies">
          <h2>Movies</h2>
          <Card />
        </section>
        <section id="series">
          <h2>TV Series</h2>
          <Card />
        </section>
      </div>
    </main>
  </div>
</template>

<script>
import Search from './components/Search.vue';
import Card from './components/Card.vue';

export default {
  name: 'App',
  components: {
    Search,
    Card,
  }
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
