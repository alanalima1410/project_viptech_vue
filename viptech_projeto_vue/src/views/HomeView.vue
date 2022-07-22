<template>
  <div class="home">
    <h1>Produtos</h1>
    <router-link to="/produto">Adicionar Produto</router-link>
    <Produto :im3="im3_src" :alt="app_name"/>
  </div>
</template>

<script>
import Produto from '../components/Produto.vue'
export default {
  components: {
    Produto
  },
  data() {
    return{
      im3_src: "/img/im3.png",
      app_name: "im3"
    }
  }
}
</script>
<style scoped>
  /* .home {

  } */

  
</style>