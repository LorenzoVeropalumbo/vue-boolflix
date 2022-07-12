<template>
  <div class="container-fluid">
    <span>Film</span>
    <div class="row row-cols-5 g-3 py-3">
      
      <div class="col" v-for="film in filmArray" :key="film.id">
        <FilmComponent :Film="film"/>
      </div>
    </div>
    <span>Serie TV</span>
    <div class="row row-cols-5 g-3 py-3">
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

  .container-fluid{
    padding: 20px 25px;
  }
</style>