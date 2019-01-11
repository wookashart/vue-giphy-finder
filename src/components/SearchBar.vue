<template>
  <div class="searchBarWrapper">
    <div class="content">
      <div class="search-bar">
        <label for="search"></label>
        <input
          type="text"
          name="search"
          id="search"
          v-model="inputValue"
        />
        <button @click="$emit('searchValue', inputValue)">Seach</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data() {
    return {
      inputValue: '',
    };
  },
}
</script>

<style lang="scss" scoped>
  @import '../scss/colors';

  .searchBarWrapper {
    background-color: $blue_dark;

    .search-bar {
      padding: 20px;
      display: flex;
      justify-content: center;

      input {
        width: 290px;
        height: 30px;
        outline: none;
        background: transparent;
        color: $white;
        border: 1px solid white;
        font-size: 18px;
        padding: 0 10px;
      }

      button {
        display: inline-block;
        height: 30px;
        padding: 0 10px;
        bottom: none;
        cursor: pointer;
      }
    }
  }
</style>
