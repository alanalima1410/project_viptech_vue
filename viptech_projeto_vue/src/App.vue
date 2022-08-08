<template>
  <div>
    <Navbar :logo="logo_src" :alt="app_name" />
    <div>
      <router-view></router-view>
    </div>
    
  </div>
</template>

<script>
import Navbar from './components/Navbar';

export default {
  components: {
    Navbar,
  },
  data() {
    return{
      logo_src: "/img/logo.png",
      app_name: "Logo"
    }
  }
}
</script>

<style>
body {
    margin: 0;
    -webkit-font-feature-settings: "lnum"; 
    -moz-font-feature-settings: "lnum"; 
    font-feature-settings: "lnum";
}



</style>
