<template>
  <div>
    <div id="nome">
      <div class="imagem">
        <img :src="im3" :alt="alt" />
      </div>
      <div class="descricao">
        <div class="produto" v-for="dado in dados" :key="dado.null">
          <h3>{{ dado.nome }}</h3>
          <p>{{ dado.marca }}</p>
          <p>R$ {{ dado.valor }},00</p>
          <p>Cor: {{ dado.cor }}</p>
          <!-- <p>{{dado.imagem}}</p> -->
          <div class="botoes"><Icons :id="dado.id "/></div>
        </div>
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
//  created() {
//     this.deleteById(id);
//   },

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
}
.imagem {
  width: 150px;
  height: 150px;
  align-items: center;
}
.descricao {
  width: 600px;
  height: 180px;
  margin-left: 50px;
}
.botoes {
  width: 250px;
  height: 180px;
  align-items: center;
  margin-top: -120px;
}
.produto {
  margin-bottom: 100px;
}
</style>
