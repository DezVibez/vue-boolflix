<template>
  <div id="app">
    <input type="text" v-model="searched" /> 
    
    <button @click="getResult()" @enter="getResult()">Cerca
    </button>

    <ul id="films" class="d-flex m-auto">
      <li v-for="movie in movies" :key="movie.id" class="cards">
        <div>
          <div>{{movie.title}} </div>
          {{movie.original_title}} 
          <div>
            <img class="poster" :src="`https://image.tmdb.org/t/p/w342/` + `${(movie.poster_path)}`" :alt="movie.title">
            <img class="flag" v-if="flags.includes(movie.original_language)" :src="flagElement(movie.original_language)">
            <span v-else>{{movie.original_language}} </span>
            <h1><font-awesome-icon icon=”faStar” /></h1>
          </div>
          
          <!--./assets/en.png-->
          {{getRating(movie)}}
          
        </div>
      </li> 
    </ul>

    <ul id="serie-tv" class="d-flex m-auto">
      <li v-for="serie in series" :key="serie.id" class="cards">
        <div>
          <div>{{serie.name}} </div>
          {{serie.original_name}} 
          <div>
            <img class="poster" :src="`https://image.tmdb.org/t/p/w342/` + `${(serie.poster_path)}`" :alt="serie.name">
            <img class="flag" v-if="flags.includes(serie.original_language)" :src="flagElement(serie.original_language)">
            <span v-else>{{serie.original_language}} </span>
          </div>
          
          <!--./assets/en.png-->
          {{getRating(serie)}}
         
        </div>
      </li>
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
      moviesEP: "/search/movie",
      seriesEP: "/search/tv",
      searched: "",
      movies: [],
      series: [],
      flags: ['it', 'en']
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
    }

    

  }
};
</script>

<style lang="scss">

.m-auto{
  margin: 0 auto;
  width: 80%;
}

ul {
  list-style-type: none;
}

img {
  height: 100px;
  width: 100px;
}

.flag{
  width: 10%;
  height: auto;
  display: block
}

.poster{
  width: 80%;
  height: auto;
  margin: 0 auto;
}

.d-flex{
  display: flex;
  flex-wrap: wrap;
}

.cards {
  color: white;
  height: 500px;
  margin: 30px;
  background-color: black;
  width: 300px;
}

</style>
