<template>
  <div class="search">
    <input type="text" v-model.trim="searchedText" @keyup.enter="search">
    <button @click="search">Search</button>
  </div>
</template>

<script>
export default {
  name: 'Search',
  data() {
    return {
      searchedText: '',
    }
  },
  methods: {
    search() {
      this.$emit('search', this.searchedText);
      this.searchedText = '';
    }
  }
}
</script>

<style scoped lang="scss">
</style>