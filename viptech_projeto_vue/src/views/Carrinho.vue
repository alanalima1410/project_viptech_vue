<template>
  <div>
    <div class="nav">
      <router-link class="link" to="/">Home</router-link>>
      <router-link class="link" to="/carrinho/:id">Carrinho</router-link>
    </div>
    <div className="titulos">
      <h1 className="title">Carrinho</h1>
      <h2 className="titlepedido">Resumo do pedido</h2>
    </div>
    <div class="conteudocarrinho">
      <div class="carrinho">
        <div class="borda">
          <div class="produto">
            <div class="getimagem">
              <img :src="this.imagem" alt="imagem" />
            </div>
            <div className="descricao">
              <h2>{{ this.nome }}</h2>
              <p>{{ this.marca }}</p>
              <p>Cor: {{ this.cor }}</p>
            </div>
          </div>

          <hr />

          <div class="quantidade">
            <div><h3>Quantidade:</h3></div>
            <div class="botoes">
              <button className="menos" v-on:click="counter -= 1">
                <svg
                  width="25"
                  height="25"
                  viewBox="0 0 32 33"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path d="M9 18.5V15.5H23V18.5H9Z" fill="#353535" />
                  <circle cx="16" cy="16.5" r="15.5" stroke="#353535" />
                </svg>
              </button>
              <div class="counter">
                <input class="number" type="text" v-model="counter" />
              </div>
              <button className="mais" v-on:click="counter += 1">
                <svg
                  width="25"
                  height="25"
                  viewBox="0 0 32 32"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M17 17.5V23.5H15V17.5H9V15.5H15V9.5H17V15.5H23V17.5H17Z"
                    fill="#353535"
                  />
                  <circle cx="16" cy="16" r="15.5" stroke="#353535" />
                </svg>
              </button>
            </div>
            <h4 class="valor">R${{ this.valor * counter }},00</h4>
          </div>
        </div>
      </div>
      <div class="borda2">
        <div class="pedido">
          <div class="subtitulo1">
            <h4>Subtotal</h4>
            <h4>R$ {{ valor * counter }}</h4>
          </div>
          <hr />
          <div id="mouse" class="subtitulo2">
            <h4>
              Frete 
              <svg id="mouse"
                width="17"
                height="14"
                viewBox="0 0 17 17"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M17 8.5C17 13.1944 13.1944 17 8.5 17C3.80558 17 0 13.1944 0 8.5C0 3.80558 3.80558 0 8.5 0C13.1944 0 17 3.80558 17 8.5Z"
                  fill="#FF6363"
                />
                <path
                  d="M9.20898 6.66016V13H7.79102V6.66016H9.20898ZM7.69727 4.99609C7.69727 4.78125 7.76758 4.60352 7.9082 4.46289C8.05273 4.31836 8.25195 4.24609 8.50586 4.24609C8.75586 4.24609 8.95312 4.31836 9.09766 4.46289C9.24219 4.60352 9.31445 4.78125 9.31445 4.99609C9.31445 5.20703 9.24219 5.38281 9.09766 5.52344C8.95312 5.66406 8.75586 5.73438 8.50586 5.73438C8.25195 5.73438 8.05273 5.66406 7.9082 5.52344C7.76758 5.38281 7.69727 5.20703 7.69727 4.99609Z"
                  fill="white"
                />
              </svg>
            </h4>
            <div id="mostrar">Valor do frete: 10% do valor do produto</div>
            <h4>R$ {{ (valor * counter) / 10 }}</h4>
          </div>
          <hr />
          <div class="subtitulo3">
            <h4>Valor</h4>
            <h4>Total R$ {{ total() }}</h4>
          </div>

          <div class="btpagar">
            <button class="btpagar" @click="toggle = !toggle">
              <svg
                class="pagar"
                width="373"
                height="47"
                viewBox="0 0 373 55"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <rect width="373" height="55" rx="7" fill="#00264B" />
                <path
                  d="M155.766 34V21.22H161.184C161.772 21.22 162.312 21.346 162.804 21.598C163.308 21.838 163.74 22.162 164.1 22.57C164.46 22.966 164.742 23.422 164.946 23.938C165.15 24.442 165.252 24.952 165.252 25.468C165.252 26.008 165.156 26.536 164.964 27.052C164.772 27.556 164.502 28.006 164.154 28.402C163.806 28.798 163.386 29.116 162.894 29.356C162.402 29.596 161.862 29.716 161.274 29.716H158.25V34H155.766ZM158.25 27.538H161.13C161.586 27.538 161.964 27.352 162.264 26.98C162.576 26.608 162.732 26.104 162.732 25.468C162.732 25.144 162.684 24.856 162.588 24.604C162.492 24.34 162.366 24.118 162.21 23.938C162.054 23.758 161.868 23.626 161.652 23.542C161.448 23.446 161.238 23.398 161.022 23.398H158.25V27.538ZM170.808 21.22H173.004L177.864 34H175.308L174.12 30.814H169.656L168.486 34H165.93L170.808 21.22ZM173.67 29.068L171.906 24.046L170.07 29.068H173.67ZM188.665 32.56C187.645 33.58 186.457 34.09 185.101 34.09C184.261 34.09 183.469 33.922 182.725 33.586C181.993 33.25 181.351 32.788 180.799 32.2C180.259 31.612 179.827 30.922 179.503 30.13C179.191 29.326 179.035 28.462 179.035 27.538C179.035 26.662 179.191 25.84 179.503 25.072C179.827 24.292 180.265 23.614 180.817 23.038C181.381 22.45 182.041 21.988 182.797 21.652C183.553 21.304 184.375 21.13 185.263 21.13C186.463 21.13 187.489 21.382 188.341 21.886C189.205 22.39 189.853 23.068 190.285 23.92L188.431 25.288C188.107 24.652 187.651 24.166 187.063 23.83C186.487 23.494 185.857 23.326 185.173 23.326C184.633 23.326 184.135 23.44 183.679 23.668C183.235 23.896 182.851 24.208 182.527 24.604C182.215 25 181.969 25.456 181.789 25.972C181.621 26.488 181.537 27.034 181.537 27.61C181.537 28.21 181.633 28.774 181.825 29.302C182.017 29.818 182.281 30.268 182.617 30.652C182.953 31.036 183.349 31.342 183.805 31.57C184.273 31.786 184.777 31.894 185.317 31.894C186.553 31.894 187.669 31.312 188.665 30.148V29.248H186.091V27.43H190.717V34H188.665V32.56ZM197.47 21.22H199.666L204.526 34H201.97L200.782 30.814H196.318L195.148 34H192.592L197.47 21.22ZM200.332 29.068L198.568 24.046L196.732 29.068H200.332ZM206.928 34V21.22H212.58C213.168 21.22 213.708 21.346 214.2 21.598C214.704 21.838 215.136 22.162 215.496 22.57C215.856 22.966 216.138 23.422 216.342 23.938C216.546 24.442 216.648 24.952 216.648 25.468C216.648 26.296 216.438 27.052 216.018 27.736C215.61 28.408 215.052 28.894 214.344 29.194L217.26 34H214.47L211.86 29.716H209.412V34H206.928ZM209.412 27.538H212.526C212.754 27.538 212.964 27.484 213.156 27.376C213.36 27.268 213.534 27.124 213.678 26.944C213.822 26.752 213.936 26.53 214.02 26.278C214.104 26.026 214.146 25.756 214.146 25.468C214.146 25.168 214.098 24.892 214.002 24.64C213.906 24.388 213.774 24.172 213.606 23.992C213.45 23.8 213.264 23.656 213.048 23.56C212.844 23.452 212.634 23.398 212.418 23.398H209.412V27.538Z"
                  fill="white"
                />
              </svg>
            </button>
          </div>
        </div>
      </div>
      <div>
        <div className="pagamento" v-show="toggle">
          <p>Pagamento realizado com sucesso!</p>
          <p>Este ...</p>
          <h2></h2>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import api from "../services/api.js";
import Pagamento from "../components/Pagamento.vue";
export default {
  components: { Pagamento },
  name: "Editar",
  componentes: {
    Pagamento,
  },
  data() {
    return {
      nome: "",
      marca: "",
      valor: 0,
      cor: "",
      id: this.$route.params.id,
      imagem: "",
      counter: 1,
      toggle: true,
      it: [],
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
    total() {
      const total =
        (this.valor * this.counter) / 10 + this.valor * this.counter;
      return total;
    },
    pagamento(total) {
      console.log(total);
      const counterCedulas = {
        200: 0,
        100: 0,
        50: 0,
        20: 0,
        10: 0,
        5: 0,
        2: 0,
      };
      var resto = total;
      for (var c = Object.keys(counterCedulas).length - 1; c >= 0; c--) {
        const currentCedula = Object.keys(counterCedulas)[c];
        const div = Math.floor(resto / currentCedula);
        counterCedulas[currentCedula] += div;
        resto -= div * currentCedula;
        Object.entries(counterCedulas).map((it) => {
          if (it[1] > 0) return ` ${it[1]} ${it[0]}`;
        });
      }
      return resto;
    },
  },
};
</script>
<style scoped>
.nav {
  margin-left: 15px;
  margin-top: 20px;
  flex-direction: row;
  display: flex;
}
.titulos {
  margin-left: 120px;
  flex-direction: row;
  justify-content: space-between;
  display: inline-flex;
  width: 1080px;
  font-family: Raleway;
}
.conteudocarrinho {
  display: flex;
  font-family: Raleway;
}
.carrinho {
  margin-left: 110px;
  display: flex;
  flex-direction: column;
  width: 812px;
  height: 260px;
  border: 1px solid gray;
  border-radius: 5px;
  padding-left: 20px;
  padding-right: 20px;
  font-family: Raleway;
}

.produto {
  height: 200px;
  display: flex;
  width: 800px;
}
.getimagem {
  align-items: center;
  display: flex;
  justify-content: center;
  padding: 25px;
  height: 150px;
  width: 150px;
}
.descricao {
  font-family: Raleway;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  align-items: center;
  height: 200px;
  width: 800px;
  margin-top: 30px;
}
.quantidade {
  font-family: Raleway;
  width: 800px;
  height: 30px;
  align-items: center;
  display: flex;
}
.botoes {
  width: 500px;
  display: flex;
}
.counter input {
  border-radius: 5px;
  display: flex;
  justify-items: center;
  text-align: center;
  align-items: center;
  margin-bottom: 10px;
  padding: 8px;
}
.menos {
  border: none;
  background: none;
}
.mais {
  border: none;
  background: none;
}
.valor {
  margin-left: 340px;
  font-family: Raleway;
  font-size: 20px;
  padding: -45px;
}

.pagar {
  width: 230px;
  margin-top: 10px;
}
.number {
  width: 20px;
  text-align: center;
  padding: 5px;
  margin-top: 12px;
}
.btpagar {
  border: none;
  align-items: center;
  text-align: center;
}
.pagamento {
  border: 1px solid #039500;
  box-sizing: border-box;
  border-radius: 7px;
  width: 425px;
  height: inherit;
  color: #039500;
  margin-left: 30px;
  position: absolute;
  right: 117px;
  top: 480px;
  margin-bottom: 30px;
  width: 265px;
  padding: 10px;
  text-align: center;
}
.linha {
  border: #ccc solid 1px;
}
.pedido {
  border: 1px solid gray;
  border-radius: 5px;
  margin-left: 20px;
  height: 260px;
  padding-left: 10px;
  padding-right: 10px;
  background: #f5f5f5;
  padding-top: 5px;
}
.pedido h4 {
  display: flex;
  justify-content: space-between;
}
.subtitulo1 {
  justify-content: space-between;
  display: flex;
  line-height: 5px;
}
.subtitulo2 {
  justify-content: space-between;
  display: flex;
  line-height: 5px;
}
.subtitulo3 {
  justify-content: space-between;
  display: flex;
  line-height: 5px;
}
#mouse{
padding-top: 5px;
}
#mouse:hover #mostrar{
  display: block;
}
#mostrar {
  display: none;
  position: absolute;
  font-size: 12px;
  background-color: white;
  flex-direction: column;
  padding: 10px;
  box-shadow: 2px 2px 2px 1px rgba(0,0,0,0.4);
  margin-top: 40px;
  font-weight: bold;

}
</style>
