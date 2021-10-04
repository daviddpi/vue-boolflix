<template>
  <header>
    <div class="d-flex align-items-center justify-content-between">
        //il click 'refresh' svuota l'array movie ritornando alla pagina principale
        <img @click="$emit('refresh')" src="../assets/logo.png" alt="Logo Boolfilx">
        //keyup invia il testo scritto dall'utente all'app
        <input class="search-film" type="text" v-model.trim="search" @keyup.enter="$emit('sendSearch', search )" placeholder="Cerca film o serie Tv">
    </div>
  </header>
</template>

<script>
export default {
    name: "Header",
    data(){
        return{
            search: "",
        }
    },
}
</script>

<style lang="scss">
@import '../style/general.scss';

header{
    background-color: black;
}

img{
    &:hover{
        cursor: pointer;
    }
}

.search-film{
    height: 20%;
    margin-right: 50px;
    background-color: $secondaryColor;
    color: white;
    font-weight: 500;
    border: none;
    border-radius: 3px;

    &:focus{
        outline: none !important;
        border:1px solid $primaryColor;
        box-shadow: 0 0 5px $primaryColor;
    }
}

</style>