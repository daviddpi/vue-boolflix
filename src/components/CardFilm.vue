<template>
    <div class="card-movie">
        <img class="mb-3 img-movie" :src="`https://image.tmdb.org/t/p/w342${imgFilm}`">

        <h5><strong>Titolo:</strong> {{ title ? title : titleSerie }}</h5>  
        <p>Titolo originale: {{original_title ? original_title : originalSerie_title}}</p>

        <div class="mb-3 d-flex">
            <p class="pe-3">Lingua:</p>
            <div v-if="lang == 'it' ">
                <img class="lang-img" src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/03/Flag_of_Italy.svg/800px-Flag_of_Italy.svg.png">
            </div>
            <div v-else-if="lang == 'en' ">
                <img class="lang-img" src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/83/Flag_of_the_United_Kingdom_%283-5%29.svg/800px-Flag_of_the_United_Kingdom_%283-5%29.svg.png">
            </div>
            <div v-else>
                {{lang}}
            </div>
        </div>

        <div class="d-flex">
            <div v-for="(starFull, index) in valutation()" :key="index">
            <i class="fas fa-star"></i>
            </div>
            <div v-for="(starEmpty, index) in (5 - valutation())" :key="(5 - index)">
            <i class="fas fa-star starEmpty"></i>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "CardFilm",

    props: {
        title: String,
        titleSerie: String,
        original_title: String,
        originalSerie_title: String,
        lang: String,
        imgFilm: String,
        voteAverage: Number,
    },

    methods: {
        valutation(){
            return Math.ceil(this.voteAverage / 2);
        }
    }

}
</script>

<style lang="scss" scoped>
@import '../style/general.scss';

.card-movie{
    color: white;
}

.img-movie{
    width: 100%;
}

.fas{
    color: $primaryColor;
    padding: 0 2px;
}

.starEmpty{
    color: rgba($primaryColor, 0.3)
}

</style>