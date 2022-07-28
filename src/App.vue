<template>
  <div id="app">
    <input type="text" v-model="searched" :key="movies.id"/> 
    
    <button @click="getMovies(); getTvSeries();">
    </button>

    <ul id="films">
      <li v-for="movie in movies" :key="movie.id">{{movie}}</li>
    </ul>

    <ul id="serie-tv">
      <li v-for="serie in series" :key="serie.id">{{serie}}</li>
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
      series: []
    };
  },

  components: {},

  methods: {
    getMovies(){
    axios
      .get(
        `${this.baseUri}/search/movie?api_key=${this.apiKey}&query=${this.searched}`
      )
      .then((response) => {
        this.movies = response.data.results;
      });
    },

    getTvSeries(){
    axios
      .get(
        `${this.baseUri}/search/tv?api_key=${this.apiKey}&query=${this.searched}`
      )
      .then((response) => {
        this.tvSeries = response.data.results;
      });
    }
    
  },
};
</script>

<style lang="scss">

</style>
