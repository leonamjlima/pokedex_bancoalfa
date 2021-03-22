
<template>
  <div id="app">
    <section id="main">

      <!-- mainHeader BEGIN -->
      <header class="mainHeader">
        <input type="text" id="edtSearch" placeholder="Search" v-model="searchText" @keyup="search">
      </header>
      <!-- mainHeader END -->

      <!-- mainArticle BEGIN -->
      <article class="mainArticle">
        <div v-for="(item, index) in pokemonListFiltered" :key="item.url">
          <div class="divPokeCard">
            <PokeCard :id="index+1" :name="item.name" :url="item.url"> </PokeCard>      
          </div>
        </div>
      </article>
      <!-- mainArticle END -->

    </section>
  </div>
</template>

<script>
import PokeCard from './components/PokeCard'
import axios from 'axios'

export default {
  name: 'App',
  data(){
    return {
      pokemonList: [],
      pokemonListFiltered: [],
      searchText: ''
    }
  },
  created: function (){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151')
      .then(response => {
        this.pokemonList = response.data.results
        this.pokemonListFiltered = response.data.results        
      })
      .catch(function (error) {
        console.log(error);
      })
  },
  components: {
    PokeCard
  },
  methods:{
    search: function(){
      this.searchText = this.searchText.toUpperCase()
      this.pokemonListFiltered = this.pokemonList;
      if (this.searchText == '' || this.searchText == ' '){
        this.pokemonListFiltered = this.pokemonList
      }else{
        this.pokemonListFiltered = this.pokemonList.filter(elemento => elemento.name.toUpperCase() == this.searchText)  
      }
    }
  },
}
</script>

<style src="./style.scss" lang="scss">
// yarn add sass-loader@^10.1.1
</style>


