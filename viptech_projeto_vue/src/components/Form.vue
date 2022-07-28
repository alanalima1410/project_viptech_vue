<template>
  <div>
    <form v-on:submit.prevent="postProduto">
      <div class="text">
        <label>Nome do produto:</label>
        <input
          type="text"
          v-model="nome"
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
        <img :src="imagem" alt="imagem">
        <input @change="handleImage" type="file" />
      </div>
      <div class="text">
        <button type="submit">Adicionar Produto</button>
      </div>
    </form>
  </div>
</template>

<script>
import api from "../services/api";
export default {
  name: "Form",
  data() {
    return {
      nome: "",
      marca: "",
      valor: 0,
      cor: "",
      imagem: ""
    };
  },
  methods: {
    postProduto() {
      api
        .post("/produto", {
          nome: this.nome,
          marca: this.marca,
          valor: this.valor,
          cor: this.cor,
          imagem: this.imagem
        
        })
        .then((res) => {
          console.log(res);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    handleImage(e) {
      const selectedImage = e.target.files[0];
      this.createBase64Image(selectedImage);
    },
    createBase64Image(fileObject){
      fileObject.text().then(()=> {
        const reader = new FileReader();
        reader.readAsDataURL(fileObject);
        reader.onload = () => {
        this.imagem = reader.result;
      };
      })
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
