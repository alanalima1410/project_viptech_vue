<template>
<div>
  <div class="home">
    <h1>Produtos</h1>
    <button class="btn" ><svg class="icone" width="15" height="15" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
<path d="M16.0016 32C7.16818 31.9903 0.00970076 24.8325 0 16V15.68C0.175908 6.88727 7.41608 -0.115241 16.2107 0.00143715C25.0053 0.118115 32.0571 7.31024 31.9997 16.1046C31.9422 24.8989 24.797 31.9982 16.0016 32ZM8.0008 14.4V17.6H14.4014V24H17.6018V17.6H24.0024V14.4H17.6018V8.00002H14.4014V14.4H8.0008Z" fill="white"/>
</svg>
<router-link class="link" to="/produto">Adicionar Produto</router-link></button>
  </div>
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
  .home h1 {
    font-family: 'Raleway';
    margin-left: 230px;
    margin-top: 70px;
  }
  .home{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }
  .link {
    list-style: none;
    text-decoration: none;
    color: white;
  }
  .btn {
    background-color: #00264B;
    width: 200px;
    height: 35px;
    color:white;
    margin-right: 170px;
    margin-top: 55px;
    font-family: 'Raleway';
    border-radius: 7px;
    font-weight: bold;
   
  }
  .icone{
    margin-right: 15px;
  }
  
</style>