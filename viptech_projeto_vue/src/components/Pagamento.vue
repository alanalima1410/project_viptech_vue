<script setup>
import { ref, onMounted }  from 'vue';

function total() {
      const total =
        (this.valor * this.counter) / 10 + this.valor * this.counter;
      return total;
    };

function pagamento(total) {
    console.log(total);
    setCedulas(true);
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
      const currentCedula = Number(Object.keys(counterCedulas)[c]);
      const div = Math.floor(resto / currentCedula);
      counterCedulas[currentCedula] += div;
      resto -= div * currentCedula;
    }
    setOpenPagar(counterCedulas);
    return resto;
  };
</script>

<template>
  
</template>
 