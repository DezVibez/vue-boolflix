<template>
  <div id="app">
    <input type="text" v-model="searched" /> 
    
    <button @click="getResult()">Cerca
    </button>

    <ul id="films" class="d-flex m-auto">
      <li v-for="movie in movies" :key="movie.id" class="cards">
        <div>
          <div>{{movie.title}} </div>
          {{movie.original_title}} 
          <div>
            <img :src="(movie.poster_path)" alt="">
            <img v-if="flags.includes(movie.original_language)" :src="flagElement(movie.original_language)">
            <span v-else>{{movie.original_language}} </span>
          </div>
          
          <!--./assets/en.png-->
          {{movie.vote_average}}
        </div>
      </li> 
    </ul>

    <ul id="serie-tv" class="d-flex m-auto">
      <li v-for="serie in series" :key="serie.id" class="cards">
        <div>
         {{serie.name}} <br>
         {{serie.original_name}} <br>
         {{serie.original_language}} <br>
        
         <!-- <img :src="flagElement(serie)"> <br>-->
         {{serie.vote_average}}
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
  height: 90px;
  width: 100px;
}

.d-flex{
  display: flex;
  flex-wrap: wrap;
}

.cards {
  height: 500px;
  margin: 30px;
  background-color: black;
  width: 300px;
}

</style>
