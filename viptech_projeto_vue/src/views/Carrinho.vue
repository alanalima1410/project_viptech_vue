<template>
<div>
    <div className="titulos">
        <h1 className="title">Carrinho</h1>
        <h2 className="titlepedido">Resumo do pedido</h2>
    </div>
    <div class="conteudocarrinho">
        <div class="carrinho">
            <div class="borda">
                <div class="getimagem">
                    <img :src="imagem" alt="imagem">
                </div>
            </div>
        </div>
    </div>
</div>
    
</template>
<script>
import api from "../services/api.js";
export default {
  name: "Carrinho",
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
//   methods: {
    
//     update() 
    
//     handleImage(e) {
//       const selectedImage = e.target.files[0];
//       this.createBase64Image(selectedImage);
//     },
//     createBase64Image(fileObject){
//       fileObject.text().then(()=> {
//         const reader = new FileReader();
//         reader.readAsDataURL(fileObject);
//         reader.onload = () => {
//         this.imagem = reader.result;
//       };
//       })
//     },
//   },
}
</script>
<style scoped>
.titulos{
    margin-top: 40px;
    margin-left: 0px;
    flex-direction: row;
    justify-content: space-between;
    display: inline-flex;
    width: 1150px;
    padding-inline-end: 250px;
}
</style>
