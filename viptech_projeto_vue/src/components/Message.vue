<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
  export default {
    name: "Message",
    props: {
      msg: String
    }
  }
</script>

<style scoped>
  .message-container {
    color: green;
    background-color: #cce5ff;
    border: 2px solid #b8daff;
    border-radius: 5px;
    width: 400px;
    margin: 30px auto;
    height: 50px;
    margin-top: 100px;
  }
</style>