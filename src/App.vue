<template>
  <div id="app">
    <!-- sendSearch prende  testo scritto dall'utente e lo manda alla funzione  che lo inserisce nella query  -->
    <Header @sendSearch="getMoviesAndSeries" @refresh="refreshPage" class="header"/>
    <!-- // refresh prende il click e con una funzione refreshPage svuota l'array -->
    <Main :movieBD="storeMovieSerie" class="main pb-4"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'
import axios from 'axios'


export default {
  name: 'App',
  components: {
    Header,
    Main,
  },

  data(){
    return{
      needle: "",
      storeMovieSerie: [],
    }
  },

  methods: {
    /**La funzione chiama un APi di film e serie tv e li inserisce nell'array storeMovieSerie
     * @param needle è il testo scritto dall'utente che viene inserito nella query per ricercare il film richiesto
     */
    getMoviesAndSeries(needle){
      const addMovie = axios.get("https://api.themoviedb.org/3/search/movie", {
        params: {
          api_key: "401d4009e7dd2687f44c4cf8d0c98098",
          language: "it-IT",
          query: needle,
        }
      });
            
      const addSeries = axios.get("https://api.themoviedb.org/3/search/tv", {
          params: {
            api_key: "401d4009e7dd2687f44c4cf8d0c98098",
            language: "it-IT",
            query: needle,
          }
      });

      axios.all([addMovie, addSeries]).then(axios.spread( (...responses) => {
        const resultOne = responses[0].data.results;
        const resultTwo = responses[1].data.results;
        // console.log("La risposta API ", responses);
        // console.log("Il primo ",resultOne);
        // console.log("Il secondo ",resultTwo);
        this.storeMovieSerie = [...resultOne, ...resultTwo];
        // console.log(this.storeMovieSerie);
      })).catch(errors => {
        console.error(errors);
      });
    },

    //la funzione che svuota l'array in modo da ricaricare la pagina
    refreshPage(){
      console.log("aggiornata la page");
      this.storeMovieSerie = [];
    }

  }
}
</script>

<style lang="scss">
@import './style/general.scss';

body{
  height: 100vh;
}

.header{
  height: max-content
}

.main{
  height: calc(100vh - 86px);
  overflow: auto;
  padding-top: 50px;
}


::-webkit-scrollbar {
  width: 10px;
}

::-webkit-scrollbar-track{
  background-color: rgb(60, 63, 63);
  border-radius: 25px;
  margin-block: 0.5rem;
}

::-webkit-scrollbar-thumb{
  background-color: rgb(156, 156, 156);
  border-radius: 25px;

}

::-webkit-scrollbar-thumb:hover{
  background-color: $primaryColor;
}


</style>