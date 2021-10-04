<template>
    <div class="bg-main">
        <div class="container">
            <div class="row g-5">
                <div class="col-12">
                    <div v-if="movieBD.length == 0" class="text-center text-white result-search">Cerca un film o una serie</div>
                    <div v-else class="text-center text-white result-search">La tua ricerca ha prodotto: {{ movieBD.length }} risultati</div>
                </div>
                <CardFilm class="col-12 col-sm-6 col-md-4 pb-2" v-for="(movie, index) in movieBD" :key="index"
                :title="movie.title" :titleSerie="movie.name"
                :original_title="movie.original_title" :originalSerie_title="movie.name"
                :lang="movie.original_language" :imgFilm="movie.backdrop_path" :voteAverage="movie.vote_average"
                :overview="movie.overview"/>
            </div>
        </div>
        
    </div>
</template>

<script>
import CardFilm from './CardFilm.vue'


export default {
    name: "Main",
    components: {
        CardFilm,
    },

    props: {
        toSearch: String,
        movieBD: Array,
    },

}
</script>

<style lang="scss">
@import '../style/general.scss';

.lang-img{
    width: 25px;
}

.bg-main{
    background-color: $secondaryColor;
}

.result-search{
    font-size: 1.5rem;
}

</style>