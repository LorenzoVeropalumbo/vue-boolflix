<template>
  <header>
    <div>
      <!-- Logo di Boolflix -->
      <img src="../assets/boolflixlogo.png" alt="">
      <!-- NAV menù -->
      <ul class="nav">
        <li>Home</li>
        <li>Serie TV</li>
        <li>Film</li>
        <li>Original</li>
        <li>Aggiunti di recente</li>
        <li>La mia lista</li>
      </ul>
    </div>
    <!-- Crezione dell side di ricerca -->
    <div class="inputs">
      <select name="" id="" >
        <option v-for="(Genre,index) in getAllGenre(this.GenreSerieArray,this.GenreFilmArray)" :key="index" value="Genre.id">{{ Genre.name }}</option>
      </select> 
      <input type="text" placeholder="cerca" v-model="searchText">
      <button @click.prevent="sendSearchText()">submit</button>
    </div>
   
   
  </header>
</template>
  
<script>
export default {
  name: "HeaderComponent",
  props:{
    GenreSerieArray:Array,
    GenreFilmArray: Array,
  },
  data(){
    return{
      searchText: '',
    }
  },
  methods: {
    sendSearchText(){
      // controllo se la input non sia vuota
      if(this.searchText !== ''){
        // poi la mando ad App.vue
        this.$emit("sendText", this.searchText);
        this.searchText = "";
      }           
    },
    getAllGenre(GenreSerieArray,GenreFilmArray){
      const ArrayToFilter = [];
      GenreSerieArray.forEach(element => {
        ArrayToFilter.push(element);
      });
      GenreFilmArray.forEach(element => {
        ArrayToFilter.push(element);
      });
      
      console.log(...new Set(ArrayToFilter))

      return [...new Set(ArrayToFilter)]
    }
  }
}
</script>

<style lang="scss" scoped>
  // Navbar Style
  header{
    height: 70px;
    background-color: #222;
    display: flex;
    justify-content: space-between;
    align-items: center;
    
    div{
      margin-left: 10px;  
      display: flex;
      
      img{
        width: 160px;
      }

      .nav{
        display: flex;
        list-style-type: none;
        align-items: center;

        li{
          padding: 0 13px;
          font-size: 18px;

          &:hover{
            font-weight: bold;
            cursor: pointer;
            font-size: 18px;
            font-weight: bold;
          }
        }      
      }
    }
    
    // Inputs Style
    .inputs{
      
      padding: 0 20px;
      
      input{
        font-size: 18px;
        padding: 0 10px;
        margin: 0 15px;
        outline: none;
      }

      button{
        font-size: 18px;
        padding: 1px 10px;
        border-radius: 5px;
      }
    }
  }
</style>