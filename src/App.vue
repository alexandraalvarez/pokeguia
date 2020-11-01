<template>
  <div id="app">
    
    <pokeguia></pokeguia>

  </div>
</template>

<script>
import pokedata from './components/Pokeguia.vue'
  export default {
    data() {
      return {
        //
      };
    },
    components: {
      'pokeguia': pokedata,
    }
  }
</script>

<style lang="scss">
* {
    margin: 0;
    padding: 0;
    background-color: #313131;
}
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
