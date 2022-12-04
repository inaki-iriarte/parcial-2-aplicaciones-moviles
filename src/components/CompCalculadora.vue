<template>
    <v-container>
        <h1>¿Cuánto es?</h1>
        <p class="subtitulo">Calculadora de impuestos en compras con moneda extranjera</p>
    </v-container>


</template>

<script>
export default {
    name: 'CompCalculadora',

    data: () => ({
      //
    }),
  }
</script>

<style>
* {
    box-sizing: border-box;
}

.container {
    font-family: 'Montserrat', sans-serif;
}

h1{
  margin: 0;
  font-weight: 700;
  font-size: 3rem;
  text-align: center;
  color: #1E1E1E;
}

.subtitulo{
  color: #154C6B;
  font-weight: 400;
  font-size: 1.5rem;
  text-align: center;
}
</style>