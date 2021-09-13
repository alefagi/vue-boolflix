<template>
  <div class="search">
    <input type="text" v-model.trim="searchedText">
    <button @click="$emit('search', searchedText)">Search</button>
  </div>
</template>

<script>
export default {
  name: 'Search',
  data() {
    return {
      searchedText: '',
    }
  }
}
</script>

<style scoped lang="scss">
</style>