<template>

  <div class="character-card">

    <!-- Immagine: -->
    <div class="img-container">
      <img :src="`${item.image}`" :alt="item.name" >
    </div>

    <!-- Personaggio: -->
    <div class="card-data">
      <h2>{{item.name}}</h2>

      <button
      @click="isModalVisible = true"
      >
      Dettagli Personaggio
      </button>

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
          class="esc">esc</button>
        </div>

        <div class="title-container">
          
          <img :src="`${item.image}`" :alt="item.name" ><br>

          <div>
            <h2>{{item.name}}</h2><br>
            <strong>Specie: </strong><span>{{item.species}}</span><br>
            <strong>Gender: </strong><span>{{item.gender}}</span><br>
            <strong>Status: </strong><span>{{item.status}}</span><br>
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
    item: Object
  },

  data(){
    return{
      isModalVisible: false
    }
  }
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

      box-shadow: 0px 1px 5px 1px #2a2a2a;

      cursor: url(@/assets/img/portal-gun.cur);

      &:active{
        transform: scale(0.9);
      }

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

  }
  


}


</style>