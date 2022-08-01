<template>
    <div className="pagamento">
          <p>Pagamento realizado com sucesso!</p>
          <h2>
            <!-- {Object.entries(openPagar).map((it) => {
              if (it[1] > 0)
                return (
                  <p>{`Este pagamento foi realizado com ${it[1]} cédulas de R$${it[0]}`}</p>
                );
            })} -->
          </h2>
        </div>
</template>

<script>

export default {
    name: "Pagamento",
    methods: {

    pagamento(total) {
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
  },
}
}
</script>

<style scoped>
.pagamento {
    border: 1px solid #039500;
    box-sizing: border-box;
    border-radius: 7px;
    width: 425px;
    height: 200px;
    color: #039500;
    margin-left: 30px;
    position: absolute;
    right: 80px;
    top: 600px;
    margin-bottom: 30px;
}
</style>