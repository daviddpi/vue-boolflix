<template>
    <div class="bg-main">
        <div class="container">
            <div class="row g-5">
                <CardFilm class="col-12 col-sm-6 col-md-4 pb-5" v-for="(movie, index) in movieBD" :key="index"
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

</style>