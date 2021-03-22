<template>
  <div class="card">
    <img class="cardImg" :src="pokePicture" alt="Avatar">    
    <div class="cardTitle">
      <div class="cardPokeName">{{ name | upper }}</div>  
      <div class="cardPokeID">#{{ id }}</div>  
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  created: function(){
    axios.get(this.url).then(res => {
      this.pokePicture = res.data.sprites.front_default
    })
  },

  /* npm install --save core-js */
  props: {
    id: Number,
    name: String,
    url: String
  },


  data(){
    return {
      pokePicture : '',
    }
  },

  filters: {
    upper: function(value){
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    }
  }

}
</script>

<style src="./style.scss" lang="scss">
</style>