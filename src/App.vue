<template>
  <div id="app">
    <input type="text" v-model="searched" :key="movies.id"/> 
    
    <button @click="getMovie">
    </button>

    <ul>
      <li v-for="movie in movies" :key="movie.id">{{movie}}</li>
    </ul>

    
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",

  data() {
    return {
      baseUri: "https://api.themoviedb.org/3",
      apiKey: "1c5e26a324a176f1263f8bbddd9a8b1f",
      searched: "",
      movies: [],
    };
  },

  components: {},

  methods: {
    getMovie(){
    axios
      .get(
        `${this.baseUri}/search/movie?api_key=${this.apiKey}&query=${this.searched}`
      )
      .then((response) => {
        this.movies = response.data.results;
      });
    }
    
  },
};
</script>

<style lang="scss">

</style>
