<template>
  <div class="film">
    <img class="film_poster" :src="getImg(Film.poster_path)" :alt="Film.title">
    <div class="hoverEffect">
      <div>
        <span>Titolo: </span>{{ Film.title }}
      </div>
      <div>
        <span>Titolo originale: </span>{{ Film.original_title }}
      </div>
      <div>
        <span>Cast: </span><span class="cast">{{ getCast(Film.id) }}</span>
      </div>
      <div>
        <img class="flags" :src="getFlags(Film.original_language)" alt="dd">
      </div>
      <div>
        <span>voto: </span>
        <span><i class="fa-solid fa-star star-space" :class="{'star': n <= getStars(Film.vote_average)}" v-for="n in 5" :key="n"></i></span>
      </div>
      <div v-if="Film.overview !== '' ">
        <span>overview: </span>
        <div class="scroll">
          <span class="overview-text">{{ Film.overview }}</span>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "FilmComponent",
  props:{
    Film:Object,
  },
  data(){
    return{
      castArray: [],
      namesCast: "",
    }
  },
  methods:{    
    getFlags(nazionalita){
      
      if(nazionalita == 'en'){
        nazionalita = "gb";
      } else if(nazionalita == 'ja'){
        nazionalita = "jp";
      } else if(nazionalita == 'hi'){
        nazionalita = "in";
      } else if(nazionalita == 'cs'){
        nazionalita = "cz";
      } else if(nazionalita == 'ko'){
        nazionalita = "kr";
      } else if(nazionalita == 'sv'){
        nazionalita = "ch";
      } else if(nazionalita == 'fa'){
        nazionalita = "af";
      }
      return `https://countryflagsapi.com/png/${nazionalita}`;
    },
    getImg(path){
      
      if(path === null){
        return 'https://adriaticaindustriale.it/wp-content/uploads/2020/02/not-found.png'
      }
      return `https://image.tmdb.org/t/p/w342${path}`
    },
    getStars(star){      
      const starcount = star/ 2;
      return Math.round(starcount);
    },
     getCast(textToSearch){  
      const search = textToSearch;
      axios.get(`https://api.themoviedb.org/3/movie/${search}/credits?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&language=en-US`)
      .then(response => {
        this.namesCast = "";
        if(response.data.cast.length > 5){
          for (let i = 0; i < 5; i++) {
            this.namesCast += response.data.cast[i].name + ", ";      
          } 
        } else if(response.data.cast.length === 0) {         
          
          this.namesCast = "no cast";

        } else {
          for (let i = 0; i < response.data.cast.length; i++) {
            this.namesCast += response.data.cast[i].name + ", ";      
          } 
        }             
      }).catch(() => {
        console.clear();
        this.namesCast = "no cast";
      })    
      return this.namesCast;         
    }
  }
}
</script>
 
<style lang="scss" scoped>
  .film{   
    height: 100%;
    position: relative;
    overflow: hidden;
    margin: 0 5px;
    cursor: pointer;

    .hoverEffect{
      position: absolute;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
      opacity: 0;
      padding: 5px 10px;

      
      div{
        text-transform: uppercase;
        padding: 8px 0 5px;

        span{
          font-weight: 800;

          &.cast{
            font-weight: 100;
            text-transform: capitalize;
            font-size: 16px;
          }
        }
      
        .scroll{
          height: 200px;
          width: 100%;  
          overflow-y: auto;

          &::-webkit-scrollbar {
            display: none;
          }

          .overview-text{
            font-weight: 100;
            text-transform: lowercase;
            font-size: 16px;
          }
        }
        
      }

      .star-space{
        padding: 0 2px;
      }
      
      .star{
        color:yellow;       
      }

      .flags{
        width: 30px;
        height: 20px;
        display: inline;
        margin: 0 5px;
      }
    }
    
    &:hover .hoverEffect{
      opacity: 1;
      background-color: rgba($color: #000000, $alpha: 0.9);
    }
    
    .film_poster{
      width: 100%;
      height: 100%;
    }
  }
</style>