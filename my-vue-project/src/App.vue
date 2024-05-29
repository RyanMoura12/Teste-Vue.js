<template>
  <v-app>
    <v-main>
      <ProductTable />
    </v-main>
  </v-app>
</template>

<script>
import ProductTable from './components/ProductTable.vue';

export default {
  name: 'App',
  components: {
    ProductTable
  }
};
</script>

<style>
/* Adicione estilos globais aqui, se necessário */
</style>
