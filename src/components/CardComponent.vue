<template>

  <div class="character-card">

    <!-- Immagine: -->
    <div class="img-container">
      <img :src="`${item.image}`" :alt="item.name" >
    </div>

    <!-- Dati: -->
    <div class="card-data">
      <h2>{{item.name}}</h2>

      <strong>Specie: </strong><span>{{item.species}}</span><br>
      <strong>Status: </strong><span>{{item.status}}</span><br>
    </div>

  </div>

</template>

<script>
export default {
  name:'CardComponent.vue',
  props: {
    item: Object
  },
}
</script>

<style lang="scss" scoped>
.character-card{
  width: 250px;
  margin-bottom: 50px;

  .img-container{
    width: 200px;
    margin-bottom: 10px;

    img{
      width: 100%;
      border-radius: 50%;
    }
  }

  .card-data{
    width: 100%;
    text-align: center;
  }

}


</style>