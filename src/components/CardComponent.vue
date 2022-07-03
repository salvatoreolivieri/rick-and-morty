<template>

  <div
   class="character-card">

    <!-- Immagine: -->
    <div class="img-container">
      <img :src="`${item.image}`" :alt="item.name" >
    </div>

    <!-- Personaggio: -->
    <div class="card-data">

        <strong>ID: </strong><span>{{item.id}}</span>
        <h2>{{item.name}}</h2>

      <!-- Botttone dettagli personaggio: -->
        <button
          @click="isModalVisible = true">

          Dettagli Personaggio
        </button>

        <br>

        <div
          v-if="!this.favouriteItems && !type">

            <button
                @click="addToFavourite(item), showPopUpAddFavourite()"
      
                id="favourite-button">
      
                  Aggiungi ai preferiti
            </button>

        </div>

        <div
          v-else>

          <!-- Bottone rimuovi preferiti: -->
            <button

              v-if="!this.favouriteItems.includes(item.id) && type"

              @click="removeFavourite(item)"

              id="favourite-button">

                Rimuovi dai preferiti

            </button>


          <!-- Bottone aggiungi preferiti: -->
            <button class="already-favourite-label"

              v-else

              @click="addToFavourite(item), showPopUpAddFavourite()"

              id="favourite-button">

              Aggiungi ai preferiti

            </button>

        </div>

    </div>

    <!-- Modal con i dati: -->
    <div
      :class="isModalVisible ? '' : 'hidden' "
      class="modal">

      <div 
        @click="isModalVisible = false"
        id="backdrop" class="backdrop">
      </div>

      <div class="details-modal">

        <div class="close-button-area">

          <button
            @click="isModalVisible = false"
            class="esc">

              esc
          </button>

        </div>

        <div class="title-container">

          <img
            :src="`${item.image}`"
            :alt="item.name" >
            
          <br>

          <div>

            <strong>ID: </strong><span>{{item.id}}</span><br>
            <h2>{{item.name}}</h2>

            <br>

            <strong>Specie: </strong><span>{{item.species}}</span>

            <br>

            <strong>Gender: </strong><span>{{item.gender}}</span>

            <br>

            <strong>Status: </strong><span>{{item.status}}</span>

            <br>

          </div>

        </div>

      </div>

    </div> 

    <!-- Modal che annuncia l'aggiunta ai preferiti -->
    <div
      :class="addedToFavourite ? '' : 'hidden' "
      class="modal">

      <div 
        @click="addedToFavourite = false"
        id="backdrop" class="backdrop">
      </div>

      <div class="details-modal favourite">

        <div class="title-container">

          <div>

            <h2>{{item.name}} aggiunto ai preferiti</h2>

            <br>

            <span>Scorri fino in fondo per vedere tutti i preferiti.</span>

          </div>

        </div>

      </div>

    </div> 

  </div>

</template>

<script>
export default {
  name:'CardComponent.vue',
  props: {
    item: Object,
    favouriteItems: Array,
    type: Boolean
  },

  data(){
    return{
      isModalVisible: false, // Utilizzo questo booleano per mostrare e nascondere il modal con i dettagli del personaggio.

      addedToFavourite: false, // Utilizzo questo booleano per mostrare e nascondere la modal che annuncia l'aggiunta di un personaggio ai preferiti.

      removeFromFavourite: false, // Utilizzo questo booleano per mostrare e nascondere la modal che annuncia la rimozione di un personaggio dai preferiti.

    }
  },

  methods:{

    addToFavourite(item){

      // Passo i parametri dal figlio al genitore per popolare l'array dei preferiti che ciclerò nel genitore:
      this.$emit('favourite', item);

      //console.log('aggiunto ai preferiti questo oggetto: ', item );

    },

    showPopUpAddFavourite(){

      // Rendo vero questo booleano per mostrare il modal che annuncia l'aggiunta ai preferiti.
      this.addedToFavourite = true;

      // Creo un timer che rende falso il precedente booleano per far scomparire automaticamente il modal.
      setTimeout(() => {
        this.addedToFavourite = false;
      }, 2000);
    },

    removeFavourite(item){

      this.$emit('removeFavourite', item);

      // console.log(this.favouriteItems?.indexOf(item));

    }

  },

}
</script>

<style lang="scss" scoped>
.character-card{
  position: relative;
  width: 250px;
  margin-bottom: 70px;

  display: flex;
  flex-direction: column;
  align-items: center;

  .img-container{
    width: 200px;
    margin-bottom: 10px;

    img{
      width: 100%;
      border-radius: 50%;
      box-shadow: 3px 5px 10px black;

    }
  }

  .card-data{
    width: 100%;
    text-align: center;

    button{
      padding: 5px 10px;
      margin-top: 10px;

      background-color: lightcoral;
      color: white;

      border: none;
      border-radius: 5px;

      cursor: pointer;

      box-shadow: 0px 1px 5px 1px #2a2a2a;

      &:active{
        transform: scale(0.9);
      }

    }

    #favourite-button{
      background-color: lightgreen;
      color: black;
    }

    .already-favourite-label{
      display: inline-block;
      margin-top: 10px;
    }

  }

  .modal {
    padding: 1rem;
    position: fixed;
    inset: 0;
    z-index: 99999;
    display: flex;
    align-items: center;
    opacity: 1;
    transition: all 0.2s;
    visibility: visible;

    &.hidden{
      opacity: 0;
      visibility: hidden;
      display: flex;
    }

    .backdrop {
      position: absolute;
      inset: 0;
      background-color: rgba(0, 0, 0, 0.5);
    }

    .details-modal {
      transition: all 0.4s;
      position: relative;
      width: 100%;
      max-width: 500px;
      margin: 0px auto;
      background-color: #ffffff;
      padding: 1rem;
      border-radius: 10px;

      h2{
        border: 20px 0;
      }

      .close-button-area{
        display: flex;
        justify-content: end;

        .esc{
          font-size: .725rem;

          color: #9CA3AF;
          background-color: #F9FAFB;

          padding: 4px;
          margin-bottom: 10px;
          width: 40px;
          border: 1px solid #dee2e6;
          border-radius: 5px;

          transition: all 0.2s;
          cursor: pointer;

          &:hover{
            color: #2a2a2a;
            box-shadow: inset  2px 2px -4px -4px #2a2a2a;
          }
        }

      }
      .title-container{

        display: flex;
        justify-content: space-around;
        align-items: center;

        img{
          width: 60%;
          border-radius: 50%;
          margin-right: 20px;
        }

        h2{
          display: inline-block;
          margin: 10px 0;
        }

        strong{
          line-height: 1.6;
        }

      }
      

    }
    .favourite{
      background-color: #3FC47B;
      box-shadow: 0px 1px 5px 1px #2a2a2a;
    }

    .removed-favourite{
      background-color: grey;
      color: white;
      box-shadow: 0px 1px 5px 1px #2a2a2a;

    }

  }
  


}


</style>