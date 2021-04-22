<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter" id="header">
      <img src="./assets/imagelogo.jpg" alt="" width="50%" height="50%" id="logo">
      <hr id="bars">
      <h3 class="is-size-3" id="title">Pokedex</h3>
      <hr id="bars">

      <input class="input is-rounded" type="text" v-model="busca" placeholder="Buscar pokemon pelo nome">
      <button class="button is-fullwidth is-primary" id="buscaBtn" @click="buscar">Buscar</button>
    </div>
    <div class="columns is-offset-one-quarter is-multiline" id="body">
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url" id="conteiner">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";
export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: "",
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=251&offset=0").then(data =>{
      console.log("Lista de pokemons adicionada")
      this.pokemons = data.data.results;
      this.filteredPokemons = data.data.results;

    })
  },
  components:{
    Pokemon
  },
  methods:{
    buscar: function(){
        this.filteredPokemons = this.pokemons;
        if (this.busca.toLowerCase() == ""|| this.busca.toLowerCase() ==" ") {
          this.filteredPokemons = this.pokemons;
        }else{
          this.filteredPokemons = this.pokemons.filter( pokemon => pokemon.name == this.busca.toLowerCase())
        }
    }
    
  },
  computed:{
    
    // resultadoBusca: function () {
      
    //   if (this.busca.toLowerCase() == ""|| this.busca.toLowerCase() ==" ") {
    //    return this.pokemons;
    //   }else{
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca.toLowerCase())
    //   }
    // }
  }
}
</script>

<style>
  @font-face {font-family: "PF Tempesta Five"; src: url("//db.onlinewebfonts.com/t/8c91fc204b5593ac86eb369e9e08cb12.eot"); src: url("//db.onlinewebfonts.com/t/8c91fc204b5593ac86eb369e9e08cb12.eot?#iefix") format("embedded-opentype"), url("//db.onlinewebfonts.com/t/8c91fc204b5593ac86eb369e9e08cb12.woff2") format("woff2"), url("//db.onlinewebfonts.com/t/8c91fc204b5593ac86eb369e9e08cb12.woff") format("woff"), url("//db.onlinewebfonts.com/t/8c91fc204b5593ac86eb369e9e08cb12.ttf") format("truetype"), url("//db.onlinewebfonts.com/t/8c91fc204b5593ac86eb369e9e08cb12.svg#PF Tempesta Five") format("svg"); }

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 30px;
  background: rgba(249,245,218,255);
  
  
   /* Center the image */
}

#buscaBtn{
  margin-top: 2%;
}

#logo{
  
}

#title{
  color: rgba(25,8,0,255);
  margin-bottom: 4%;
  
  font-family: "PF Tempesta Five";
  
}
#conteiner{
    column-count: gap;
  column-span: all;
  
  
}

#bars{
  background-color: rgb(164,116,12);
}

#header{}

#body{
  align-items: center;
  align-content: center;
  
  width: 100%;
  margin-left: 3.5%;
  background: rgba(249,245,218,255);

}

</style>
