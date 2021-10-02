<template>
  <div id="app">
    <input type="text" v-model="search" @keyup.enter="sendSearch">
    <div>
      <div v-for="(movie, index) in storeMovie" :key="index">
        {{ movie.title }} , {{movie.original_title}} , {{movie.vote_averange}}
        <div v-if="confirmImg(movie)">
          <img :src="movie.original_language | convertFlag()" alt="">
        </div>
        <div v-else>
          {{movie.original_language | convertFlag() }}
        </div>
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
      storeMovie: [],
    }
  },

  methods: {

    getMovies(){
      axios.get("https://api.themoviedb.org/3/search/movie", {
        params: {
          api_key: "401d4009e7dd2687f44c4cf8d0c98098",
          query: this.search,
        }
      })
      .then( (response) => {
        const result = response.data.results;
        console.log(response);
        this.storeMovie = result.slice();
        console.log(this.storeMovie);
      })
    },

    sendSearch(){
      console.log(this.search);
      this.getMovies();
      
    },

    /**
     * La funziona passa il valore TRUE in caso la condizione sia verificata, il valore FALSO se non viene verificata
     * @param item è l'array passato, in questo caso movie
     */
    confirmImg(item){
      if(item.original_language == "it" || item.original_language == "en" || 
      item.original_language == "de" || item.original_language == "fr" || item.original_language == "es"){
        return true;
      }
      return false;
    }
    
  },

  
  filters: {
    
    /** La funziona verifica se il valore str chiamato è uguale ad uno dei casi, se è vero la funziona ritorna
     * la funzione sotto forma di bandiera, in caso contrario ritornerà solo il nome in forma scritta.
     * @param str è il valore passato "original language" preso dalla chiatama
     */
    convertFlag(str){

      switch (str){
        case "it":
          str = "https://upload.wikimedia.org/wikipedia/commons/thumb/0/03/Flag_of_Italy.svg/800px-Flag_of_Italy.svg.png";
          return str

        case "en":
          str = "https://upload.wikimedia.org/wikipedia/commons/thumb/8/83/Flag_of_the_United_Kingdom_%283-5%29.svg/800px-Flag_of_the_United_Kingdom_%283-5%29.svg.png";
          return str

        case "de":
          str = "https://upload.wikimedia.org/wikipedia/commons/thumb/b/ba/Flag_of_Germany.svg/1280px-Flag_of_Germany.svg.png";
          return str;

        case "fr":
          str = "https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Flag_of_France.svg/1280px-Flag_of_France.svg.png";
          return str;
        
        case "es":
          str = "https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Flag_of_Spain.svg/1280px-Flag_of_Spain.svg.png";
          return str;
        
        default:
          return str;
      }
    }
  },

}
</script>

<style lang="scss">
@import './style/general.scss';

img{
  width: 25px;
}

</style>
