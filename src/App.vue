<template>
  <div id="app">

    <div class="nav">

      <div>
        <h1>
          NETFLIX
        </h1>
      </div>


      <div>
        <input type="text" v-model="searched" @keyup.enter="getResult()" /> 
    
        <button @click="getResult()">Cerca
        </button>
      </div>

    

    </div>

    <main>

      <ul id="films" class="d-flex m-auto">
        <li v-for="movie in movies" :key="movie.id" class="cards">
          <div class="visibility">
            <div class="poster">
              <img class="poster-image" v-if="movie.poster_path" :src="`https://image.tmdb.org/t/p/w342/` + `${(movie.poster_path)}`" :alt="movie.title">
              <img class="not-found" v-else src="./assets/imageNotFound.jpeg" :alt="movie.title">
            </div>

            <div class="infos">

              <div>{{movie.title}} </div>
              <div>{{movie.original_title}} </div>

              <img class="flag" v-if="flags.includes(movie.original_language)" :src="flagElement(movie.original_language)">
              <span v-else>Linguaggio originale: {{movie.original_language}} </span>
              
              
              <span>Rating: {{getRating(movie)}}</span>
            </div>
            
          </div>
        </li> 
      </ul>

      <ul id="serie-tv" class="d-flex m-auto">
        <li v-for="serie in series" :key="serie.id" class="cards">
          <div class="visibility">
            <div class="poster">
              <img class="poster-image" v-if="serie.poster_path" :src="`https://image.tmdb.org/t/p/w342/` + `${(serie.poster_path)}`" :alt="serie.name">
              <img class= "not-found" v-else src="./assets/imageNotFound.jpeg" alt="">
              
            </div>

            <div class="infos">
              <div>{{serie.name}} </div>
              <div>{{serie.original_name}} </div>

              <img class="flag" v-if="flags.includes(serie.original_language)" :src="flagElement(serie.original_language)">
              <span v-else>Linguaggio originale: {{serie.original_language}} </span>
            
            
              <span>Rating: {{getRating(serie)}}</span>
            </div>
            
          
          </div>
        </li>
      </ul>

    </main>

    
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
      moviesEP: "/search/movie",
      seriesEP: "/search/tv",
      searched: "",
      movies: [],
      series: [],
      flags: ['it', 'en'],
    };
  },

  components: {
  
    
    },

  methods: {
    flagElement(lang){
      
      return require(`./assets/${lang}.png`)
    },
    getResult(){
    axios
      .get(
        `${this.baseUri}${this.moviesEP}?api_key=${this.apiKey}&query=${this.searched}`+
        `${this.baseUri}${this.seriesEP}?api_key=${this.apiKey}&query=${this.searched}`
      )
      .then((response) => {
        this.movies = response.data.results;
        this.series = response.data.results;
      });
    },
    getRating(rate){
     
     let rateResult = Math.floor((rate.vote_average) / 2)

     if (rateResult == 0 ) {rateResult == rateResult + 1}

     else return rateResult
    },


    

  }
};
</script>

<style lang="scss">

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.nav{
  padding: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100px;
  background-color: black;
}

.nav input{
  margin: 0 10px;
}

h1{
  font-size: 30px;
  color: red;
}

main {
  background-color:rgb(37, 37, 41);;
  min-height: 100vh;
}

.m-auto{
  margin: 0 auto;
  width: 80%;
}

ul {
  list-style-type: none;
}

.flag{
  width: 10%;
  height: auto;
  display: block
}

.poster{
  position: absolute
}

.poster img{
  height: 428px;
  width: 279px;
}

.poster-image {
  background-position: cover;
}

.visibility:hover .poster{
  display: none
}

.infos {
  display: none;
}

.infos {
  display: inline-block;
  width: 100%;
  height: 100%;
}

.not-found{
  height: 428px;
  width: 279px;
}

.d-flex{
  display: flex;
  flex-wrap: wrap;
}

.cards {
  border: 1px solid white;
  color: white;
  padding: 10px;
  margin: 30px;
  background-color: black;
  width: 300px;
  height: 450px;
}

</style>
