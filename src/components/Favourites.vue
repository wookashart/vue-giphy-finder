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
  }
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
    
    > div {
      padding: 15px;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
      background-color: $blue_light;
    }

    img {
      max-width: 100%;
    }
  }
</style>
