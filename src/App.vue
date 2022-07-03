<template>

  <div>

    <HeaderComponent
      @search="startSearch"

    />

    <MainComponent
      :charactersSearched="charactersSearched"
    />

    <FooterComponent />

  </div>

</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue';
import MainComponent from './components/MainComponent.vue';
import FooterComponent from './components/FooterComponent.vue';

import axios from "axios"

export default {
  name: 'App',
  components: {
    HeaderComponent,
    MainComponent,
    FooterComponent
  },

  data(){
    return{
      apiUrl: 'https://rickandmortyapi.com/api/character/?name=',
      apiParameters:{
        name: ""
      },
      charactersSearched:[]
    }
  },

  methods:{

    // Richiesta Api con la query che digita l'utente nell'input di ricerca:
    apiRequestFromQueryToSearch(){

      axios.get(this.apiUrl + this.apiParameters.name)
      .then(output => {

        // console.log(output.data.results);

        this.charactersSearched = output.data.results;

      })
      .catch(error =>{
        console.log(error);
      })

    },

    startSearch(inputToSearch){

      // Il parametro della chiamata Api diventa l'input di ricerca:
      this.apiParameters.name = inputToSearch;

      // invochiamo la funzione della chiamta Api:
      this.apiRequestFromQueryToSearch()
    }
  },

}
</script>

<style lang="scss">

@import './assets/style/global';
@import './assets/style/var';

</style>
