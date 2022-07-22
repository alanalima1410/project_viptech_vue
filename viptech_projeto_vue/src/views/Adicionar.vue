<template>
  <div class="adicionar">
    <h1>Adicionar Produto</h1>
    <Form />
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
