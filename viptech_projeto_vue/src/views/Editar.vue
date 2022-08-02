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
          <select v-model="cor">
          <option disabled value="">Selecione a cor</option>
          <option>Branco</option>
          <option>Cinza</option>
          <option>Preto</option>
        </select>
        </div>
        <div class="text">
          <label>Data de Cadastro</label>
          <input type="date" placeholder="00/00/0000" />
        </div>
        <div class="text">
          <button class="btn-img-bt"><img :src="imagem" alt="imagem"><svg width="103" height="90" viewBox="0 0 103 90" fill="none" xmlns="http://www.w3.org/2000/svg">
<path d="M81.5417 26.2501V37.4626C81.5417 37.4626 73.0012 37.5001 72.9583 37.4626V26.2501H60.0833C60.0833 26.2501 60.1262 18.7876 60.0833 18.7501H72.9583V7.50012H81.5417V18.7501H94.4167V26.2501H81.5417ZM68.6667 41.2501V30.0001H55.7917V18.7501H21.4583C16.7375 18.7501 12.875 22.1251 12.875 26.2501V71.2501C12.875 75.3751 16.7375 78.7501 21.4583 78.7501H72.9583C77.6792 78.7501 81.5417 75.3751 81.5417 71.2501V41.2501H68.6667ZM21.4583 71.2501L34.3333 56.2501L42.9167 67.5001L55.7917 52.5001L72.9583 71.2501H21.4583Z" fill="#D9D9D9"/>
</svg><input  class="btn-img" @change="handleImage" type="file" />
</button>
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
.btn-img {
  width: 130;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  
}
.btn-img-bt{
  width: 130px;
  height: 130px;
  object-fit: contain;
  border: none;
}
</style>
