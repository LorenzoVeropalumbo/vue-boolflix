<template>
  <div class="container">
    <div class="row row-cols-4 g-5">
      <div class="col" v-for="film in filmArray" :key="film.id">
        <FilmComponent :Film="film"/>
      </div>
    </div>
  </div>
</template>

<script>
  import FilmComponent from './FilmComponent.vue'
  export default {
    name: "FilmsMainComponent",
    components: {
      FilmComponent,
    },
    props:{
      filmArray: Array,
    }
  }
</script>

<style lang="scss" scoped>
  .container{
    padding-top: 60px;
  }
</style>