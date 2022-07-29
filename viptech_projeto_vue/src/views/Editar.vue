<template>
  <div class="editar">
    <div class="nav">
          <router-link class="link" to="/">Home</router-link>>
          <router-link class="link" to="/editar/:id">Editar Produto</router-link>
      </div>
    <h1>Editar produto</h1>

    <div id="form">
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
          <img :src="imagem" alt="imagem">
          <input @change="handleImage" type="file" />
        </div>
        <div class="text">
          <button class="submit-btn" type="submit">SALVAR PRODUTO</button>
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
      imagem: "",
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
          this.imagem = res.data.imagem;
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
  max-width: 550px;
  margin: 0 auto;
  font-family: 'Raleway';
 
}
.text {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
   
}
label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
}
input, select {
  padding: 5px 10px;
}

.submit-btn {
  background-color: #00264B;
  width: 150px;
  height: 35px;
  color: blanchedalmond;
}
.editar {
  font-family: 'Raleway';
}
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
}

</style>
