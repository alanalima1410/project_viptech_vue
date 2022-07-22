<template>
  <div>
    <div id="nav">
      <router-link id="logo-url" to="/">
        <img :src="logo" :alt="alt">
      </router-link>
      <!-- <router-link to="/">Home</router-link>
      <router-link to="/adicionar">Adicionar Produto</router-link>
      <router-link to="/editar">Editar Produto</router-link> -->
    </div>
  </div>
</template>

<script>

export default {
    name: "Navbar",
    props: ["logo", "alt"]
}
</script>

<style scoped>

#nav {
    background-color: #00264B;
    margin: 0px;
    padding: 20px;
    text-align: center;
    height: 44px;
}

</style>