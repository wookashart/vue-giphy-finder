<template>
  <div id="app">
    <search-bar @searchValue="searchValue" />
    <results :results="results" @searchGifs="searchGifs" />
    <favourites :favourites="favourite" @searchGifs="searchGifs" />
  </div>
</template>

<script>
import SearchBar from '@/components/SearchBar';
import Results from '@/components/Results';
import Favourites from '@/components/Favourites';

const api_key = 'EwQCHDTYU2onchg4pwYQmRFRcugz5ySa';
const trendingGiphsAPI = `http://api.giphy.com/v1/gifs/trending?api_key=${api_key}&limit=16`;
const searchAPI = `http://api.giphy.com/v1/gifs/search?api_key=${api_key}`;

export default {
  name: 'app',
  data() {
    return {
      value: '',
      results: [],
      favourite: [],
    }
  },
  components: {
    'search-bar': SearchBar,
    'results': Results,
    'favourites': Favourites,
  },
  methods: {
    searchValue(value) {
      this.value = value;
    },
    searchGifs() {
      this.favourite = JSON.parse(localStorage.getItem('favouritesGiphy'));

      fetch(this.value === "" ? trendingGiphsAPI : `${searchAPI}&q=${this.value}`)
      .then(res => res.json())
      .then(res => {
        if (this.favourite !== null) {
          res.data.map(gif => {
            this.favourite.map(fav => {
              if (gif.id === fav.id) {
                gif.inFavourite = true;
              };
            });
          });
        };
        this.results = res.data;
      })
      .catch(err => {
        console.log(err);
      });
    },
  },
  beforeMount() {
    this.favourite = JSON.parse(localStorage.getItem('favouritesGiphy'));

    fetch(trendingGiphsAPI)
      .then(res => res.json())
      .then(res => {
        if (this.favourite !== null) {
          res.data.map(gif => {
            this.favourite.map(fav => {
              if (gif.id === fav.id) {
                gif.inFavourite = true;
              };
            });
          });
        };
        this.results = res.data;
      })
      .catch(err => {
        console.log(err);
      });
  },
}
</script>

<style lang="scss">
  @import './scss/colors';

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

  .VueCarousel-navigation-button {
    display: none;
    top: -20px !important;
    font-size: 16px;
    background-color: $blue_light !important;

    @media (min-width: 1024px) {
      display: block;
    }

    &.VueCarousel-navigation-prev {
      left: 83px;
    }

    &.VueCarousel-navigation-next {
      right: 57px;
    }

    &:focus {
      outline: none !important;
    }
  }

  .VueCarousel-dot {
    &:focus {
      outline: none !important;
    }
  }
</style>
