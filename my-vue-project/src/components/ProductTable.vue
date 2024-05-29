<template>
  <v-container>
    <v-data-table
      :search="search"
      :headers="headers"
      :items="products"
      :items-per-page="5"
      class="elevation-1"
      :footer-props="{
          showFirstLastPage: false,
          'items-per-page-text':'linhas por página',
          itemsPerPageOptions:[5,10,20,30,40,50,500]
      }"
      sort-by="calories"
          no-data-text="Nenhum registro disponível"
          no-results-text="Nenhum registro encontrado"
        >
        <template v-slot:top>
            <v-toolbar flat color="white">
              <v-toolbar-title></v-toolbar-title>
              <v-text-field
                class="mr-3"
                outlined
                dense
                v-model="search"
                append-icon="mdi-magnify"
                label="Busca"
                single-line
                full-width
                hide-details
              ></v-text-field>
            </v-toolbar>
          </template>
    
      <template v-slot:item="{ item }">
        <tr>
          <td>
            <v-img :src="item.src" height="80" width="80"></v-img>
          </td>
          <td>{{ item.variants[0].value }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.categories[0].name }}</td>
        </tr>
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
import axios from 'axios';

export default {
  name: 'ProductTable',

  data() {
    return {
      headers: [
        { text: 'Imagem', value: 'src' },
        { text: 'Tamanhos', value: 'variants[0].value' },
        { text: 'Nome do Produto', value: 'name' },
        { text: 'Categorias', value: 'categories[0].name' },
      ],
      products: [],
      search: "",
    };
  },
  mounted() {
    this.fetchProducts();
  },

  methods: {
    async fetchProducts() {
      const url = 'https://apibgdev.nswebservice.com.br/store/10/products';
      const postData = {
      };

      try {
        const response = await axios.post(url, postData);
        this.products = response.data
      } catch (error) {
        console.error('Erro ao buscar produtos:', error.response ? error.response.data : error.message);
      }
    },
  },
};
</script>