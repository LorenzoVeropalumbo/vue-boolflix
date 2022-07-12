<template>
  <div class="container">
    <div class="row row-cols-4 g-2">
      <div class="col" v-for="film in filmArray" :key="film.id">
        <FilmComponent :Film="film"/>
      </div>
      <div class="col" v-for="serie in serieArray" :key="serie.id">
        <serieComponent :Serie="serie"/>
      </div>
    </div>
  </div>
</template>

<script>
  import serieComponent from './serieComponent.vue';
  import FilmComponent from './FilmComponent.vue';
  
  export default {
    name: "BoolflixComponent",
    components: {
      FilmComponent,
      serieComponent,
    },
    props:{
      filmArray: Array,
      serieArray: Array,
    }
  }
</script>

<style lang="scss" scoped>
  .container{
    padding: 60px 0;
  }
</style>