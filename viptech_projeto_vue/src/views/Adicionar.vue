<template>
<div>
  <div class="nav">
          <router-link class="link" to="/">Home</router-link>>
          <router-link class="link" to="/produto">Adicionar Produto</router-link>
      </div>
  <div class="adicionar">
    <h1>Adicionar Produto</h1>
    <Form />
  </div>
</div>
</template>
<script>
import api from '../services/api.js';
import Form from '../components/Form.vue';
export default {
  name: "Adicionar",
  components: {
        Form
    },
}
</script>
<style scoped>
h1 {
    font-family: 'Raleway';
    margin-left: 390px;
    margin-top: 60px;
    margin-bottom: 50px;
  }
  .nav {
  margin-left: 15px;
  margin-top: 20px;
  flex-direction: row;
  display: flex;
  font-family: 'Raleway';
}
</style>