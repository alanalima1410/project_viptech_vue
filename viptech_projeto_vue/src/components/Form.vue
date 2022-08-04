<template>
  <div id="form">
    <form v-on:submit.prevent="postProduto">
      <div class="text-t">
        <label>Nome do produto:</label>
        <input
          type="text-t"
          v-model="nome"
          placeholder="Digite o nome do produto"
          required
        />
      </div>
      <div class="text-t">
        <label>Marca:</label>
        <input
          type="text"
          v-model="marca"
          placeholder="Digite a marca do produto"
          required
        />
      </div>
      <div class="text">
        <label>Valor:</label>
        <input type="number" v-model="valor" placeholder="R$00,00" required />
      </div>
      <div class="text">
        <label>Cor:</label>
        <select class="text" v-model="cor" required>
          <option disabled value="">Selecione a cor</option>
          <option>Branco</option>
          <option>Cinza</option>
          <option>Preto</option>
        </select>
      </div>
      <div class="text">
        <label>Data de Cadastro:</label>
        <input
          type="date"
          :value="
            myDate &&
            new Date(myDate.getTime() - myDate.getTimezoneOffset() * 60 * 1000)
              .toISOString()
              .split('T')[0]
          "
          @input="myDate = $event.target.valueAsDate"
          required
        />
      </div>
      <div class="text">
        <div>
          <img class="btn-img" src="../assets/iconeimg.svg" />
          <input class="btn" @change="handleImage" type="file" required />
        </div>
        <div v-if="imagem != null">
          <img :src="imagem" />
        </div>
      </div>
      <div class="text">
        <button class="submit-btn" type="submit">
          ADICIONAR PRODUTO
          <Message :msg="msg" v-show="msg" />
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import api from "../services/api";
import Message from "../components/Message.vue";

export default {
  name: "Form",
  data() {
    return {
      nome: "",
      marca: "",
      valor: 0,
      cor: "",
      imagem: "",
      date: new Date().toISOString().substr(0, 10),
      msg: null,
    };
  },
  components: {
    Message,
  },
  methods: {
    postProduto() {
      api
        .post("/produto", {
          nome: this.nome,
          marca: this.marca,
          valor: this.valor,
          cor: this.cor,
          imagem: this.imagem,
        })
        .then((res) => {
          console.log(res);
          this.msg = "Produto adicionado com sucesso!";
            window.location.reload();
        })

        .catch((error) => {
          console.log(error);
          this.msg = "Falha ao adicionar produto!";
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
  font-family: "Raleway";
  border-radius: 7px;
  font-weight: bold;
}
.btn-img {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  cursor: pointer;
  z-index: 1;
  width: 150px;
}
.btn {
  opacity: 0;
}
.text input,
select {
  border-radius: 4px;
  -moz-border-radius: 4px;
  -webkit-border-radius: 4px;
  box-shadow: 1px 1px 2px;
  -moz-box-shadow: 1px 1px 2px;
  -webkit-box-shadow: 1px 1px 2px;
  border: 1px solid #00264b;
  width: 350px;
  height: 32px;
  margin-bottom: 2px;
  
}
.text input,
select[type="text"]:hover,
textarea:hover {
  background: #ffffff;
  border: 1px solid #00264b;
}
.text select {
  height: 43px;
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
  margin-bottom: 8px;
  margin-top: 20px;
}
</style>
