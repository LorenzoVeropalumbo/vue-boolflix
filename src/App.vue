<template>
  <div id="app">
    <headerComponent 
    @sendText="searchText"
    />
  </div>
</template>

<script>
import headerComponent from './components/headerComponent.vue'
import axios from "axios"

export default {
  name: 'App',
  data(){
    return{
      info: [],
      textToSearch: "",
    }
  },
  components: {
    headerComponent,
  },
  mounted(){
    this.searchAllFilms();  
  },
  methods: {    
    searchAllFilms(){
      
      if(this.textToSearch !== ""){
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&query=${this.textToSearch}&language=it-IT`)
        .then(response => {
        
          this.info = response.data.results;
          return console.log(this.info)
        })
      } else {
        axios.get(`https://api.themoviedb.org/3/movie/top_rated?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&language=it-IT&page=1`)
        .then(response => {
          
          this.info = response.data.results;
          return console.log(this.info)
        })
      }     
    },
    searchText(text){
      this.textToSearch = text;
      console.log(text);
      this.searchAllFilms(); 
    }
  }
}
</script>

<style lang="scss">

</style>
