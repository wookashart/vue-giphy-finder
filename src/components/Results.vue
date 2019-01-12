<template>
  <div class="resultsWrapper">
    <div class="content">
      <ul class="giphs-list">
        <li v-for="(item, index) in this.results" :key="index">
          <div>
            <img :src="item.images.fixed_height_downsampled.url" />
          </div>
          <span v-if="!item.inFavourite" class="add-to-favourite" @click="addToFavourite(item)"><i class="fas fa-plus"></i>Add to favourites</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Results',
  props: {
    results: {
      type: Array,
      required: true,
    }
  },
  methods: {
    addToFavourite(item) {
      const storedFavourites = JSON.parse(localStorage.getItem('favouritesGiphy')) !== null
          ? JSON.parse(localStorage.getItem('favouritesGiphy'))
          : [];
      const newItem = {
        id: item.id,
        gif: item.images.fixed_height_downsampled.url,
      };

      storedFavourites.push(newItem);

      localStorage.setItem('favouritesGiphy', JSON.stringify(storedFavourites));
      this.$emit('searchGifs');
    },
  },
}
</script>

<style lang="scss" scoped>
  @import '../scss/colors';

  .giphs-list {
    list-style: none;
    padding: 0;
    display: grid;
    grid-template-columns: 1fr;
    grid-column-gap: 15px;
    grid-row-gap: 15px;

    @media (min-width: 768px) {
      grid-template-columns: 1fr 1fr;
    }

    @media (min-width: 1024px) {
      grid-template-columns: 1fr 1fr 1fr 1fr;
    }

    li {
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: $blue_light;
      padding: 15px;
      padding-bottom: 30px;
      position: relative;

      div {
        height: auto;
        
        img {
          max-width: 100%;
          max-height: 100%;
        }
      }
      
      .add-to-favourite {
        position: absolute;
        right: 10px;
        bottom: 5px;
        transition: 0.1s linear;
        cursor: pointer;

        i {
          margin-right: 5px;
        }

        &:hover {
          color: $blue_dark;
        }
      }
    }
  }
</style>
