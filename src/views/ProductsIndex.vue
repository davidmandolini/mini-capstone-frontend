<script>
import axios from "axios";
export default {
  data: function () {
    return {
      products: [],
    };
  },
  created: function () {
    this.productsIndex();
  },
  methods: {
    productsIndex: function () {
      axios.get("/products").then((response) => {
        this.products = response.data;
        console.log(response.data);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>Products</h1>
    <div><a v-bind:href="`/products/new`">Create New Product</a></div>
    <div v-for="product in products" v-bind:key="product.id">
      <h2>{{ product.name }}</h2>
      <p>Price: ${{ product.price }}</p>
      <a v-bind:href="`/products/${product.id}`">More Info</a>
    </div>
  </div>
</template>

<style></style>
