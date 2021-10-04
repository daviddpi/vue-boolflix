<template>
    <div>
        <img :src="`https://image.tmdb.org/t/p/w342${imgFilm}`" alt="">

        <div>
            {{ title ? title : titleSerie }}  
        </div>
        <div>
            {{original_title ? original_title : originalSerie_title}}
        </div>
        <div v-if="lang == 'it' ">
            <img class="lang-img" src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/03/Flag_of_Italy.svg/800px-Flag_of_Italy.svg.png">
        </div>
        <div v-else-if="lang == 'en' ">
            <img class="lang-img" src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/83/Flag_of_the_United_Kingdom_%283-5%29.svg/800px-Flag_of_the_United_Kingdom_%283-5%29.svg.png">
        </div>
        <div v-else>
            {{lang}}
        </div>
        <div class="d-flex">
            <div v-for="(starFull, index) in valutation" :key="index">
            <i class="fas fa-star"></i>
            </div>
            <div v-for="(starEmpty, index) in (5 - valutation)" :key="(5 - index)">
            <i class="far fa-star"></i>
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
        valutationStar: Function,
    },

}
</script>

<style>

</style>