<template>
  <div class="editar">
    <h1>Editar produtos</h1>
    <Form />
  </div>
</template>
<script>
import api from '../services/api.js';
import Form from '../components/Form.vue';
export default {
  name: "Editar",
  components: {
        Form
    },
}
</script>