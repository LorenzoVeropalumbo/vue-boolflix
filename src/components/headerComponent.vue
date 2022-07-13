<template>
  <header>
    <div>
      <h1>boolflix</h1>
      <ul class="nav">
        <li>Home</li>
        <li>Serie TV</li>
        <li>Film</li>
        <li>Original</li>
        <li>Aggiunti di recente</li>
        <li>La mia lista</li>
      </ul>
    </div>
    <div class="inputs"> 
      <input type="text" placeholder="cerca" v-model="searchText">
      <button @click.prevent="sendSearchText()">submit</button>
    </div>
   
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
    background-color: #222;
    display: flex;
    justify-content: space-between;
    align-items: center;
    div{
      
      display: flex;
      
      h1{
        text-transform: uppercase;
        font-size: 40px;
        padding: 0 20px;
        color: red;  
        margin: 0;
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