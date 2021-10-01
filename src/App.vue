<template>
  <div id="app">
    <input type="text" v-model="search" @keyup.enter="sendSearch">
    <div v-if="storeMovie.length > 0">
      <div v-for="(movie, index) in storeMovie" :key="index">
        {{ movie.title }} , {{movie.original_title}} ,{{movie.original_language}} , {{movie.vote_averange}}<br>
      </div>
    </div>
    <div v-else>
      <p>Non ci sono risultati</p>
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
    
  }
}
</script>

<style lang="scss">
@import './style/general.scss';


</style>
