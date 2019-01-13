<template>
  <div class="favouritesWrapper" v-if="favourites">
    <div class="content">
      <h2>Favourites</h2>
      <Carousel
        :navigationEnabled="true"
        :perPageCustom="[[320, 1], [768, 2], [1024, 4]]"
        :scrollPerPage="true"
        :navigationNextLabel="'Next'"
        :navigationPrevLabel="'Previous'"
      >
        <Slide v-for="(item, index) in favourites" :key="index">
          <div>
            <img :src="item.gif" />
          </div>
          <span class="remove-from-favourite" @click="removeFromFavourite(item)">
            <i class="fas fa-times"></i>
          </span>
        </Slide>
      </Carousel>
    </div>
  </div>
</template>

<script>
import { Carousel, Slide } from 'vue-carousel';

export default {
  name: 'Favourites',
  components: {
    Carousel,
    Slide
  },
  props: {
    favourites: {
      type: Array,
    }
  },
  methods: {
    removeFromFavourite(item) {
      const storedFavourites = JSON.parse(localStorage.getItem('favouritesGiphy'));

      storedFavourites.map((gif, index) => {
        if (gif.id === item.id) {
          storedFavourites.splice(index, 1);
        };
      });

      localStorage.setItem('favouritesGiphy', JSON.stringify(storedFavourites));
      this.$emit('searchGifs');
    },
  },
}
</script>

<style lang="scss" scoped>
  @import '../scss/colors';

  .favouritesWrapper {
    background-color: $blue_dark;
    padding: 20px 0;

    h2 {
      color: $white;
      text-align: center;
      margin: 0;
      margin-bottom: 20px;
    }
  }

  .VueCarousel-slide {
    padding: 7.5px;
    position: relative;
    
    > div {
      padding: 15px;
      padding-top: 30px;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
      background-color: $blue_light;
    }

    img {
      max-width: 100%;
    }

    .remove-from-favourite {
      position: absolute;
      top: 10px;
      right: 15px;
      cursor: pointer;
      font-size: 20px;
    }
  }
</style>
