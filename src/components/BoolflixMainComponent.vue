<template>
  <div class="container-fluid">
    <div class="sectionTitle">Film</div>
    <div class="row row-cols-5 py-1 horizonal-scroll">
      
      <div class="col" v-for="film in filmArray" :key="film.id">
        <FilmComponent :Film="film"/>
      </div>
    </div>
    <div class="sectionTitle">Serie TV</div>
    <div class="row row-cols-5 py-1 horizonal-scroll">
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
      textToSearch: String,
    }
  }
</script>

<style lang="scss" scoped>

  .container-fluid{
    padding-bottom: 80px;

    .sectionTitle{
      font-size: 30px;
      margin: 10px 15px;
      font-weight: 600;
    }

    .horizonal-scroll{
      height: calc(60% - 40px);
      flex-wrap: nowrap;
      overflow-x: auto;
      overflow-y: hidden;
      margin: 0 10px;
      flex-shrink: 0;
      
      &::-webkit-scrollbar {
        width: 10px;
        height: 22px;
      }

      &::-webkit-scrollbar-thumb:hover {
        background-color: grey;
      }

      &::-webkit-scrollbar-thumb {
        background-color: #222;
        border-radius: 20px;
        border: 6px solid transparent;
        background-clip: content-box;
      }
      
      .col{
        padding: 0;
      }
    }
  }
</style>