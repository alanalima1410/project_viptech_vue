<template>
  <div>
    
    <div>
      
        <div  id="nome" v-for="dado in dados" :key="dado.null">
          <div class="imagem">
          <img :src="dado.imagem" alt="imagem">
          </div>
          <div class="descricao">
            <h3>{{ dado.nome }}</h3>
            <p>{{ dado.marca }}</p>
            <p class="cif">R$ {{ dado.valor }},00</p>
            <p>Cor: {{ dado.cor }}</p>
          </div>
          <div class="botoes"><Icons :id="dado.id "/></div>
        </div>
      </div>
    </div>
  
</template>

<script>
import Icons from "../components/Icons.vue";
import api from "../services/api.js";

export default {
  name: "Produto",
  components: {
    Icons,
  },
  props: ["im3", "alt"],
  data() {
    return {
      dados: null,
      id: Number,
    };
  },
  created() {
    this.getProduto();
  },

  methods: {
    getProduto() {
      api
        .get("/produto")
        .then((res) => {
          this.dados = res.data;
          console.log(this.dados);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    
  },
};
</script>

<style scoped>
#nome {
  display: flex;
  flex-direction: row;
  margin-top: 50px;
  height: 100%;
  width: 100%;
  justify-content: center;
  font-family: 'Raleway';
}
.imagem {
  width: 150px;
  height: 180px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}
.descricao {
  width: 600px;
  height: 180px;
  margin-left: 50px;
}
.botoes {
  /* width: 250px; */
  height: 180px;
  align-items: center;
  /* margin-top: -120px; */
}
.produto {
  margin-bottom: 100px;
}
.cif {
  color: #0F4C81;
  font-weight: bold;
  font-size: 20px;
  
}
</style>
