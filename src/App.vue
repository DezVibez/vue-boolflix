<template>
  <div id="app">
    
    
  </div>
</template>

<script>
import axios from "axios"


export default {
  name: 'App',
  data(){
    return {
      baseUri: "https://api.themoviedb.org/3",
      apiKey: "1c5e26a324a176f1263f8bbddd9a8b1f",
      queryValue: "anelli"
    }

  },
  components: {},
  created(){
    axios.get("baseUri/search/movie?api_key=apiKey&query=anelli")
  }
}
</script>

<style lang="scss">
#app {
  
}
</style>
