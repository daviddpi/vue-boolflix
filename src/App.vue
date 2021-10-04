<template>
  <div id="app">
    <Header @sendSearch="TakenSearch" />
    <Main :toSearch="needle" />

  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'


export default {
  name: 'App',
  components: {
    Header,
    Main,
  },

  data(){
    return{
      needle: "",
    }
  },

  methods: {
    TakenSearch(needle){
      console.log(needle);
    },

  }
}
</script>

<style lang="scss">
@import './style/general.scss';

</style>