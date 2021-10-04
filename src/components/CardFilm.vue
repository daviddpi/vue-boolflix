<template>
    <div class="card-movie">
        <img v-if="imgFilm != null" class="mb-3 img-movie" :src="`https://image.tmdb.org/t/p/w342${imgFilm}`">
        <img v-else src="https://dummyimage.com/334x366/000000/db202c&text=BOOLFIX" alt="image boolfix">
        
        <div class="info-card">
            <h5><strong>Titolo:</strong> {{ title ? title : titleSerie }}</h5>  
            <p><strong>Titolo originale:</strong> {{original_title ? original_title : originalSerie_title}}</p>

            <div class="d-flex">
                <p class="pe-3"><strong>Lingua: </strong></p>
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

            <div class="d-flex mb-3">
                <div v-for="(starFull, index) in valutation()" :key="index">
                <i class="fas fa-star"></i>
                </div>
                <div v-for="(starEmpty, index) in (5 - valutation())" :key="(5 - index)">
                <i class="fas fa-star starEmpty"></i>
                </div>
            </div>
            <p><strong>Overview:</strong> {{ overview | cutString() }}</p>
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
        overview: String
    },

    methods: {
        valutation(){
            return Math.ceil(this.voteAverage / 2);
        }
    },

    filters: {
        cutString(str){
            if(str.length > 300){
                return str.slice(0, 300) + "...";
            }
            return str;
        }
    }

}
</script>

<style lang="scss" scoped>
@import '../style/general.scss';

.card-movie{
    color: white;
    border: 3px solid $secondaryColor;
    padding-top: 20px;
    height: 440px;

    // .img-movie{
    //     width: 100%;
    //     height: 100%;
    //     object-fit: fill;
    // }

    // &:hover{
    //     .info-card{
    //         display: block;
    //     }

    //     .img-movie{
    //         display: none;
    //     }
    // }
}

// .info-card{
//     display: none;
// }

//animation
.img-movie{
    display: block;
    width: 100%;
    height: 100%;
    object-fit: fill;
}

.card-movie{
    position: relative;
}

.card-movie:hover .info-card {
    -webkit-transform: scale(1);
    -ms-transform: scale(1);
    transform: scale(1);
}

.info-card {
    position: absolute;
    padding: 20px;
    bottom: 0;
    left: 0;
    right: 10;
    background-color: rgb(0, 0, 0);
    overflow: hidden;
    width: 100%;
    height: 100%;
    -webkit-transform: scale(0);
    -ms-transform: scale(0);
    transform: scale(0);
    -webkit-transition: .3s ease;
    transition: .3s ease;
}
//end animation

.fas{
    color: $primaryColor;
    padding: 0 2px;
}

.starEmpty{
    color: rgba($primaryColor, 0.3)
}

</style>