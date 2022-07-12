<template>
  <div class="film">
    <div><span>{{ Film.title }}</span></div>
    <div><span>{{ Film.original_title }}</span></div>
    <div><span>{{ Film.original_language }}</span></div>
    <div><span>{{ Film.vote_average }}</span></div>
  </div>
</template>

<script>
export default {
  name: "FilmComponent",
  props:{
    Film:Object,
  }
}
</script>
 
<style lang="scss" scoped>
  .film{
    padding: 5px;
    border: 1px solid white;
    height: 100%;

    div{
      text-align: center;
      text-transform: uppercase;
    }
  }
</style>