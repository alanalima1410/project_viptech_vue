<template>
  <div class="editar">
    <h1>Editar produtos</h1>

    <div>
      <form @submit="update">
        <div class="text">
          <label>Nome do produto:</label>
          <input
            type="text"
            v-model="this.nome"
            placeholder="Digite o nome do produto"
          />
        </div>
        <div class="text">
          <label>Marca</label>
          <input
            type="text"
            v-model="marca"
            placeholder="Digite a marca do produto"
          />
        </div>
        <div class="text">
          <label>Valor</label>
          <input type="number" v-model="valor" placeholder="R$00,00" />
        </div>
        <div class="text">
          <label>Cor</label>
          <input
            type="text"
            v-model="cor"
            placeholder="Digite a cor do produto"
          />
        </div>
        <div class="text">
          <label>Data de Cadastro</label>
          <input type="date" placeholder="00/00/0000" />
        </div>
        <div class="text">
          <input type="file" />
        </div>
        <div class="text">
          <button type="submit">Adicionar Produto</button>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import api from "../services/api.js";
export default {
  name: "Editar",
  data() {
    return {
      nome: "",
      marca: "",
      valor: 0,
      cor: "",
      id: this.$route.params.id,
    };
  },
  mounted() {
      api
        .get("/produto/" + this.id)
        .then((res) => {
          this.nome = res.data.nome;
          this.marca = res.data.marca;
          this.valor = res.data.valor;
          this.cor = res.data.cor;
          console.log(res);
        })
        .catch((error) => {
          console.log(error);
        });
  },
  methods: {
    
    update() {
      api
        .put("/produto/" + this.id, {
          nome: this.nome,
          marca: this.marca,
          valor: this.valor,
          cor: this.cor,
        })
        .then((res) => {
          console.log(res);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
<style scoped>
#form {
  max-width: 400px;
  margin: 0 auto;
}
.text {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}
label {
  font-weight: bold;
  margin-bottom: 15px;
}
</style>
