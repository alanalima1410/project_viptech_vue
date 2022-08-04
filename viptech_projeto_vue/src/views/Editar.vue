<template>
  <div class="editar">
    <div class="nav">
      <router-link class="link" to="/">Home</router-link>>
      <router-link class="link" to="/editar/:id">Editar Produto</router-link>
    </div>
    <h1>Editar produto</h1>

    <div id="form">
      <form @submit="update">
        <div class="text-t">
          <label>Nome do produto:</label>
          <input
            type="text"
            v-model="this.nome"
            placeholder="Digite o nome do produto"
            required
          />
        </div>
        <div class="text-t">
          <label>Marca</label>
          <input
            type="text"
            v-model="marca"
            placeholder="Digite a marca do produto"
            required
          />
        </div>
        <div class="text">
          <label>Valor</label>
          <input type="number" v-model="valor" placeholder="R$00,00" required />
        </div>
        <div class="text">
          <label>Cor do produto:</label>
          <input
            type="text"
            v-model="this.cor"
            placeholder="Digite a cor do produto"
            required
          />
        </div>
        <div class="text">
          <label>Data de Cadastro</label>
          <input type="date" placeholder="00/00/0000" required />
        </div>
        <div class="text">
          <button class="btn-img-bt">
            <img :src="imagem" alt="imagem" />
            <input class="btn-img" @change="handleImage" type="file" required />
          </button>
        </div>
        <div class="text">
          <button class="submit-btn" type="submit">
            SALVAR PRODUTO
            <Message :msg="msg" v-show="msg" />
          </button>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import api from "../services/api.js";
import Message from "../components/Message";
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
      msg: null,
    };
  },
  components: {
    Message,
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
          this.msg = "Produto atualizado com sucesso!";
            window.location.reload();
        })
        .catch((error) => {
          console.log(error);
        });
    },
    handleImage(e) {
      const selectedImage = e.target.files[0];
      this.createBase64Image(selectedImage);
    },
    createBase64Image(fileObject) {
      fileObject.text().then(() => {
        const reader = new FileReader();
        reader.readAsDataURL(fileObject);
        reader.onload = () => {
          this.imagem = reader.result;
        };
      });
    },
  },
};
</script>
<style scoped>
#form {
  max-width: 550px;
  margin: 0 auto;
  font-family: "Raleway";
  margin-left: 250px;
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
input,
select {
  padding: 5px 10px;
}

.submit-btn {
  background-color: #00264b;
  width: 150px;
  height: 35px;
  color: blanchedalmond;
  border-radius: 7px;
  font-weight: bold;
  font-family: "Raleway";
}
.editar {
  font-family: "Raleway";
}
h1 {
  font-family: "Raleway";
  margin-left: 390px;
  margin-top: 60px;
  margin-bottom: 50px;
  margin-left: 250px;
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
  opacity: 0;
  margin-bottom: 15px;
}
.btn-img-bt {
  width: 130px;
  height: 130px;
  object-fit: contain;
  border: none;
}
.text input {
  border-radius: 4px;
  -moz-border-radius: 4px;
  -webkit-border-radius: 4px;
  box-shadow: 1px 1px 2px;
  -moz-box-shadow: 1px 1px 2px;
  -webkit-box-shadow: 1px 1px 2px;
  border: 1px solid #00264b;
  width: 350px;
  height: 32px;
  margin-bottom: 3px;
}
.text input[type="text"]:hover,
textarea:hover {
  background: #ffffff;
  border: 1px solid #00264b;
}
.text-t input {
  border-radius: 4px;
  -moz-border-radius: 4px;
  -webkit-border-radius: 4px;
  box-shadow: 1px 1px 2px;
  -moz-box-shadow: 1px 1px 2px;
  -webkit-box-shadow: 1px 1px 2px;
  border: 1px solid #00264b;
  width: 550px;
  height: 32px;
  margin-bottom: 10px;
  margin-top: 15px;
}
</style>
