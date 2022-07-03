<template>

  <main>

    <div>
      
      <div class="title-container">
        <h1>Personaggi Cercati</h1>

        <span
          v-if="this.charactersSearched.length === 0">
          Le tue ricerche appariranno qui.
        </span>
      </div>

       <div class="card-container">

        <!-- Componente card che cicla i personaggi contenuti nel mio Array -->
        <CardComponent
          @favourite="addToFavourite"
          @removeFavourite="removeFromFavourite"
          v-for="(object, index) in this.charactersSearched"
          :key="`all${index}`"
          :item="object"/>

       </div>

    </div>

    <!-- Tutti i personaggi -->
    <div class="title-container">
      <h1>Tutti i personaggi</h1><br>
    </div>

    <div class="card-container">

      <!-- Componente card che cicla i personaggi contenuti nel mio Array -->
      <CardComponent
        @favourite="addToFavourite"
        @removeFavourite="removeFromFavourite"

        v-for="(object, index) in this.characters"
        :key="`all${index}`"
        :item="object"
        :type="false"
        />
        
    </div>

    <!-- Personaggi Preferiti -->
    <div class="title-container" id="favourites">
      <h1>Personaggi preferiti</h1>
    </div>

    <div class="card-container">

      <CardComponent
        v-for="(object, index) in this.favouriteCharacters"
        @removeFavourite="removeFromFavourite"

        :key="`favourite${index}`"
        :item="object"
        :favouriteItems = 'favouriteCharacters'
        :type="true"
        />
    </div>

  </main>

</template>

<script>

import axios from "axios";
import CardComponent from "./CardComponent.vue";


export default {
  name: 'MainComponent.vue',
  props:{
    charactersSearched: Array
  },

  components: { CardComponent },

  data(){
    return {
      // Dati relativi alla chiama API:
      apiUrl: "https://rickandmortyapi.com/api/character",
      characters:[],
      info: '',
      favouriteCharacters: [],
    }
  },

  methods:{

    // Eseguo la Chiamata Api di tutti i personaggi:
    apiRequestAll(){
      axios.get(this.apiUrl)
      .then(output =>{
        //console.log('questo è il log dei personaggi: ', output.data.results);
        this.characters = output.data.results;
      })

      // Qui gestisco l'errore:
      .catch(error =>{
        console.log(error);
      })
    },

    // Eseguo la Chiamata Api di tutti i personaggi:
    apiRequestByQuery(){
      axios.get(this.apiUrl)
      .then(output =>{
        //console.log('questo è il log dei personaggi: ', output.data.results);
        this.filtertedCharacters = output.data.results;
      })

      // Qui gestisco l'errore:
      .catch(error =>{
        console.log(error);
      })
    },

    //Aggiungo l'elemento ai preferiti
    addToFavourite(item){

        if (this.favouriteCharacters.includes(item)) {
          //console.log('utente già nei preferiti');
        } else{

          this.favouriteCharacters.push(item)


        }

        // Aggiungo l'elemento al mio array dei preferiti che poi ciclerò:
        // this.favouriteCharacters.push(item)

        //console.log('questo elemento è stato aggiunto ai preferiti:', this.favouriteCharacters);
    },

    //Rimuovo l'elemento ai preferiti
    removeFromFavourite(item){
        this.favouriteCharacters.splice(this.favouriteCharacters.indexOf(item), 1)
        //console.log(this.favouriteCharacters.indexOf(item));
        

    }

  },

  mounted(){
    // Invoco la chiamato Api di tutti i personaggi: 
    this.apiRequestAll()


  },

}
</script>

<style lang="scss" scoped>

main{
  scroll-behavior: smooth;
  padding: 50px;

  .card-container,
  .title-container{
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;

    width: 80%;
    margin: 0 auto;
    text-align: center;

    .hidden{
      display: none;
    }

    span{
      display: inline-block;
      margin-top: 10px;
    }

    a{
      margin-top: 15px;
    }
  }

  .title-container{
    flex-direction: column;
  }

  .card-container{
    margin-top: 50px;
  }

}

</style>