<template>
  <div class="film">
    <img class="film_poster" :src="getImg(Film.poster_path)" alt="">
    <div class="hoverEffect">
      <div><span>Titolo: </span>{{ Film.title }}</div>
      <div><span>Titolo originale: </span>{{ Film.original_title }}</div>
      <div><span>{{ Film.original_language }}: </span><img class="flags" :src="getFlags(Film.original_language)" alt="dd"></div>
      <div><span>voto: </span><span class="star" v-for="n in 10" :key="n">{{ Film.vote_average }}</span></div>
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
      }
      return `https://countryflagsapi.com/png/${nazionalita}`;
    },
    getImg(path){
      if(path === null){
        return 'https://adriaticaindustriale.it/wp-content/uploads/2020/02/not-found.png'
      }
      return `https://image.tmdb.org/t/p/w342${path}`
    }
  }
}
</script>
 
<style lang="scss" scoped>
  .film{
    border: 1px solid white;
    height: 100%;
    position: relative;

    .hoverEffect{
      position: absolute;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
      opacity: 0;
      padding: 10px;
      
      div{
        text-transform: uppercase;
        padding: 5px 0;

        span{
          font-weight: 800;
        }

        .star{

        }
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