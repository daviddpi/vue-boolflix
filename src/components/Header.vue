<template>
  <header>
    <div class="d-flex align-items-center justify-content-between">
        <img src="../assets/logo.png" alt="Logo Boolfilx">
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

header{
    background-color: black;
}

.search-film{
    height: 20%;
    margin-right: 50px;

}

</style>