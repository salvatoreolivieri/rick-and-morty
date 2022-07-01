<template>

<header>

  <div class="logo-container">
    <img src="../assets/img/logo.jpg" alt="">
  </div>

  <div>
    <input type="text" placeholder="Cerca personaggio..">
  </div>

</header>
  
</template>

<script>
export default {
  name:'HeaderComponent.vue'
}
</script>

<style lang="scss" scoped>

@import "../assets/style/var";

header{

  display: flex;
  justify-content: space-between;
  align-items: center;

  height: 100px;
  padding: 0px 50px;

  background-color: #F8F9FA;
  border-bottom: 1px solid $border-color;

  .logo-container{
    width: 100px;

    img{
      width: 100%;
      cursor: pointer;
    }

  }

  input{
    border: 1px solid $border-color;
    border-radius: 5px;
    outline: none;
    padding: 5px;
  }

}

</style>