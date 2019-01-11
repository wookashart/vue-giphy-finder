<template>
  <div class="resultsWrapper">
    <div class="content">
      <ul class="giphs-list">
        <li v-for="(item, index) in this.results" :key="index">
          <div>
            <img :src="item.images.downsized_medium.url" />
          </div>
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
  }
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

      div {
        height: auto;
        
        img {
          max-width: 100%;
          max-height: 100%;
        }
      }
    }
  }
</style>
