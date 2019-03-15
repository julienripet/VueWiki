<template>
  <header>
    <h1>{{titre}}</h1>
    <form v-on:submit="getValue">
      <label for="searchBox">Faire votre recherche : </label>
      <input ref="searchBox" id="searchBox" name="searchBox" type="text"/>
      <button type="submit" v-on:submit='getValue' name="btnSearch"> recherche </button>
    </form>
  </header>
</template>

<script>
import {bus} from './event.js';

export default {
  data () {
    name: 'searchedText'
    return {
      searchedText : '',
      titre: 'Recherche wikipedia'
    }
  },
  methods:{
    getValue: function(e){
      bus.$emit('textentered',this.$refs.searchBox.value)
      e.preventDefault()
      //console.log(e)
    }
  }
}
</script>

<style scoped>
  header{
    background-color: lightgrey;
    max-width: 900px;
    position: relative;
    margin: 20px auto;
    padding:20px;
    border-radius: 5px;
}

  h1{
    margin: 20px auto;
  }

  button{
    margin:auto;
  }
</style>
