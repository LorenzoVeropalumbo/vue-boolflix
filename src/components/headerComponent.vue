<template>
  <header>
    <input type="text" placeholder="cerca" v-model="searchText"
    >
    <button @click.prevent="sendSearchText()">submit</button>
  </header>
</template>

<script>
export default {
  name: "headerComponent",
  data(){
    return{
      searchText: '',
    }
  },
  methods: {
    sendSearchText(){
      if(this.searchText !== ''){
        this.$emit("sendText", this.searchText);
        this.searchText = "";
      }           
    }
  }
}
</script>

<style lang="scss" scoped>
  header{
    height: 70px;
    color: ;
  }
</style>