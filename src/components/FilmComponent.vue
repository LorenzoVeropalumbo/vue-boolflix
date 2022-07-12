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
        <span>{{ Film.original_language }}: </span>
        <img class="flags" :src="getFlags(Film.original_language)" alt="dd">
      </div>
      <div>
        <span>voto: </span>
        <span><i class="fa-solid fa-star star" v-for="n in getStars(Film.vote_average)" :key="n"></i></span>
      </div>
      <div>
        <span>overview: </span>
        <div class="scroll">
          <span class="overview-text">{{ Film.overview }}</span>
        </div>
      </div>
    </div>

  </div>
</template>

<script>

export default {
  name: "FilmComponent",
  props:{
    Film:Object,
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
      console.log(starcount)
      return Math.round(starcount);
    }
  }
}
</script>
 
<style lang="scss" scoped>
  .film{
    border: 1px solid white;
    height: 100%;
    position: relative;
    overflow: hidden;

    .hoverEffect{
      position: absolute;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
      opacity: 0;
      padding: 5px;
      
      div{
        text-transform: uppercase;
        padding: 8px 0 5px;

        span{
          font-weight: 800;
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