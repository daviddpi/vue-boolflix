<template>
    <div class="card-movie">
        <!-- l'API che non contiene un poster viene sostituita da un'immagine -->
        <img v-if="imgFilm != null" class="mb-3 img-movie img-fluid" :src="`https://image.tmdb.org/t/p/w342${imgFilm}`">
        <img v-else class="img-movie img-fluid" src="https://dummyimage.com/342x191/000000/db202c&text=BOOLFIX" alt="image boolfix">
        
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
                <div v-else class="lang">
                    {{lang}}
                </div>
            </div>

            <div class="d-flex mb-3">
                <div v-for="(starFull, index) in valutation()" :key="'starFull'+index">
                <i class="fas fa-star"></i>
                </div>
                <div v-for="(starEmpty, index) in (5 - valutation())" :key="'starEmpty'+index">
                <i class="fas fa-star starEmpty"></i>
                </div>
            </div>
            <p><strong>Trama:</strong> {{ overview }}</p>
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

}
</script>

<style lang="scss" scoped>
@import '../style/general.scss';

.card-movie{
    color: white;
    border: 3px solid $secondaryColor;
    padding-top: 20px;
}

//animation
.img-movie{
    display: block;
    width: 100%;
    height: 100%;
    object-fit: fill;
    border: 2px solid black;
    box-shadow: 0 0 25px black;
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
    padding: 15px;
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
    overflow: auto;
    box-shadow: 0 0 25px black;
}

//end animation

.fas{
    color: $primaryColor;
    padding: 0 2px;
}

.starEmpty{
    color: rgba($primaryColor, 0.3)
}

.lang{
    text-transform: uppercase;
}

// @media screen and (min-width: 992px){
    
//     //animation
//     .img-movie{
//         display: block;
//         border: 2px solid black;
//         box-shadow: 0 0 25px black;

//         &:hover{
//             box-shadow: 0 0 25px $primaryColor;
//         }
//     }

//     .card-movie:hover .info-card {
//         width: 25%;
//         left: 75%;
//     }

//     .info-card {
//         position: fixed;
//         padding: 15px;
//         top: 86px;
//         bottom: 0;
//         left: 100%;
//         right: 10;
//         background-color: rgba(0, 0, 0, .8);
//         overflow: hidden;
//         width: 0;
//         height: 100%;
//         transition: .3s ease;
//         overflow: auto;
//         z-index: 2;
//         -webkit-transform: none;
//         -ms-transform: none;
//         transform: none;
//         -webkit-transition: .3s ease;
//     }
//     //end animation
// }

</style>