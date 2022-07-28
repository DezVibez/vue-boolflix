<template>
  <div id="app">
    
    
  </div>
</template>

<script>
import axios from "axios"


export default {
  name: 'App',
  
  components: {},
  created(){
    axios.get(`${this.baseUri}/search/movie?api_key=${this.apiKey}&query=${this.queryValue}`)
    .then(response => {
      this.movies = response.data.results}

      
      
    )
  },
  data(){
    return {
      baseUri: "https://api.themoviedb.org/3",
      apiKey: "1c5e26a324a176f1263f8bbddd9a8b1f",
      queryValue: "",
      movies: [],
    }

  },
}
</script>

<style lang="scss">
#app {
  
}
</style>
