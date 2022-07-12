<template>
  <div id="app">
    <headerComponent 
    @sendText="searchText"
    />

    <main>
      <FilmsMainComponent :filmArray="this.filmArray"/>
    </main>

  </div>
</template>

<script>
import headerComponent from './components/headerComponent.vue'
import FilmsMainComponent from './components/FilmsMainComponent.vue'
import axios from "axios"

export default {
  name: 'App',
  data(){
    return{
      filmArray: [],
      textToSearch: "",
    }
  },
  components: {
    headerComponent,
    FilmsMainComponent,
  },
  mounted(){
    this.searchAllFilms();  
  },
  methods: {    
    searchAllFilms(){
      
      if(this.textToSearch !== ""){
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&query=${this.textToSearch}&language=it-IT`)
        .then(response => {        
          this.filmArray = response.data.results;
        })
      } else {
        axios.get(`https://api.themoviedb.org/3/movie/top_rated?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&language=it-IT&page=1`)
        .then(response => {       
          this.filmArray = response.data.results;
        })
      }     
    },
    searchText(text){
      this.textToSearch = text;
      this.textToSearch = this.textToSearch.replace(" ","+")
      this.searchAllFilms(); 
    }
  }
}
</script>

<style lang="scss">
  @import "src/style/common.scss";
  #app{
    height: 100vh;
    width: 100%;
    background-color: grey;
  }
</style>
