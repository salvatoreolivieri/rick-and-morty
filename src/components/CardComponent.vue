<template>

  <div>
    <!-- Immagine: -->
    <img :src="`${item.image}`" :alt="item.name" >

    <!-- Dati: -->
    <h3>{{item.name}}</h3>
    <strong>Specie: </strong><span>{{item.species}}</span><br>
    <strong>Status: </strong><span>{{item.status}}</span><br>
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

</style>