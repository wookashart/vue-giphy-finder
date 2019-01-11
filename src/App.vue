<template>
  <div id="app">
    <search-bar @searchValue="searchValue" />
    <results :results="results" />
  </div>
</template>

<script>
import SearchBar from '@/components/SearchBar';
import Results from '@/components/Results';

const api_key = 'EwQCHDTYU2onchg4pwYQmRFRcugz5ySa';
const trendingGiphsAPI = `http://api.giphy.com/v1/gifs/trending?api_key=${api_key}&limit=20`;

export default {
  name: 'app',
  data() {
    return {
      results: [],
    }
  },
  components: {
    'search-bar': SearchBar,
    'results': Results,
  },
  methods: {
    searchValue(value) {
      console.log(value);
    },
  },
  beforeMount() {
    fetch(trendingGiphsAPI)
      .then(res => res.json())
      .then(res => {
        this.results = res.data;

        console.log(res.data);
      })
      .catch(err => {
        console.log(err);
      });
  },
}
</script>

<style lang="scss">
  * {
    box-sizing: border-box;
    font-family: 'Oswald', sans-serif;
  }

  html,
  body {
    margin: 0;
    padding: 0;
  }

  .content {
    max-width: 1100px;
    margin: auto;
  }
</style>
