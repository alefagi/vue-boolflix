<template>
  <div>
    <input type="text" v-model="searchedText">
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
  button {
    padding: 5px;
    margin-left: 10px;
    color: #fff;
    background-color: red;
  }

  input {
    padding: 5px;
  }
</style>