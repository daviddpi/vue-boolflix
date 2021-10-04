<template>
  <div id="app">
    <input type="text" v-model.trim="search" @keyup.enter="sendSearch">
    <div>
      <div v-for="(movie, index) in storeMovieLang" :key="index">

        <img :src="`https://image.tmdb.org/t/p/w342${movie.backdrop_path}`" alt="">
        <div>
          {{ movie.title ? movie.title : movie.name }} , {{movie.original_title ? movie.original_title : movie.original_name}} , {{movie.vote_average}}
          <div v-if="movie.showFlag != index">
            <img :src="`https://www.countryflags.io/${movie.original_language}/flat/24.png`" @error="imgNotFound(index)">
          </div>
          <div v-else>
            {{movie.original_language}}
          </div>
        </div>
        <hr>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  components: {
    
  },
  data(){
    return{
      search: "",
      storeMovieSerie: [],
    }
  },

  methods: {
    getMoviesAndSeries(){
      const addMovie = axios.get("https://api.themoviedb.org/3/search/movie", {
          params: {
            api_key: "401d4009e7dd2687f44c4cf8d0c98098",
            query: this.search,
          }
        });
      
      const addSeries = axios.get("https://api.themoviedb.org/3/search/tv", {
        params: {
            api_key: "401d4009e7dd2687f44c4cf8d0c98098",
            query: this.search,
          }
      });
      axios.all([addMovie, addSeries]).then(axios.spread( (...responses) => {
        const resultOne = responses[0].data.results;
        const resultTwo = responses[1].data.results;
        console.log("La risposta API ", responses);
        console.log("Il primo ",resultOne);
        console.log("Il secondo ",resultTwo);
        this.storeMovieSerie = [...resultOne, ...resultTwo];
        this.storeMovieSerie.forEach( element => {
          element.showFlag = -1;
        })
        console.log(this.storeMovieSerie);
      })).catch(errors => {
        console.error(errors);
      });
    },
    sendSearch(){
      console.log(this.search);
      this.getMoviesAndSeries();
    },

    imgNotFound(index){
      this.storeMovieSerie[index].showFlag = index;
    }
  },
  
  computed: {
    /**
     * La funzione converte la lingua nella bandiera corretta da visualizzare
     */
    storeMovieLang(){

      return this.storeMovieSerie.filter( str => {
        switch(str.original_language){
          case "en":
            return str.original_language ="gb";
  
          case "ja":
            return str.original_language = "jp";
  
          case "ko":
            return str.original_language = "kr";
  
          case "zh":
            return str.original_language = "cn";
          
          case "hi":
            return str.original_language = "in";
  
          case "ur":
            return str.original_language = "in";
  
          case "uk":
            return str.original_language = "in";
          
          case "cs":
            return str.original_language = "cz";
  
          case "ar":
            return str.original_language = "ae";
  
          default:
            return str.original_language;
        }
      })
    }
  }
}
</script>

<style lang="scss">
@import './style/general.scss';


</style>