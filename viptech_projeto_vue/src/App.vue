<template>
  <div>
    <Navbar :logo="logo_src" :alt="app_name" />
    <div>
      <router-view></router-view>
    </div>
    <Footer />
  </div>
</template>

<script>
import Navbar from './components/Navbar';
import Footer from './components/Footer';

export default {
  components: {
    Navbar,
    Footer
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
}



</style>
