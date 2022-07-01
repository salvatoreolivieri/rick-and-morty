<template>

  <main>

    <div class="card-container">
      <!-- Componente card che clica i personaggi contenuti nel mio Array -->
      <CardComponent
      v-for="(object, index) in this.characters"
      :key="index"
      :item="object"
      />
    </div>

  </main>

</template>

<script>

import axios from "axios";
import CardComponent from "./CardComponent.vue";

export default {
  name: 'MainComponent.vue',
  components: { CardComponent },

  data(){
    return {
      // Dati relativi alla chiama API
      apiUrl: "https://rickandmortyapi.com/api/character",
      characters:[],
    }
  },

  methods:{
    // Chiamata Api 
    apiRequest(){
      axios.get(this.apiUrl)
      .then(output =>{
        console.log('questo è il log dei personaggi: ', output.data.results);
        this.characters = output.data.results;
      })
    },

  },

  mounted(){
    // Invoco la chiamato Api 
    this.apiRequest()
  }
}
</script>

<style lang="scss" scoped>

main{

  padding: 50px;

  .card-container{
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;

    width: 80%;
    margin: 0 auto;
  }

}

</style>