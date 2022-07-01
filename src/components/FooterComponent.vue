<template>
  <footer>
    <span>Developer with enthusiasm by Salvatore Olivieri </span>
  </footer>
</template>

<script>
export default {
  name:'FooterComponent.vue'
}
</script>

<style lang="scss" scoped>

@import "../assets/style/var";

footer{
  height: 100px;
  width: 80%;
  margin: 0 auto;

  display: flex;
  justify-content: center;
  align-items: center;

  border-top: 1px solid $border-color;

}

</style>