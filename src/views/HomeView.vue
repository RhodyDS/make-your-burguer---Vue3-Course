<template>
  <div class="main-container">
    <Banner />
    <h1>Monte o seu hamburguer:</h1>
    <BurguerForm/>

  </div>

</template>

<script>
import Banner from '../components/Banner.vue'
import BurguerForm from '../components/BurguerForm.vue'

export  default{
  name: "Home",
  components:{
    Banner,
    BurguerForm
  }
}
</script>

<style scoped>

h1 {
   padding: 2rem;
}
</style>
