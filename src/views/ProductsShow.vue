<script>
import axios from "axios";
export default {
  data: function () {
    return {
      product: {},
      cartedProductParams: {
        product_id: parseInt(this.$route.params.id),
        quantity: 1,
      },
    };
  },
  created: function () {
    this.productsShow();
  },
  methods: {
    productsShow: function () {
      axios.get("/products/" + this.$route.params.id).then((response) => {
        console.log(this.cartedProductParams);
        console.log(response, "HI");
        this.product = response.data;
      });
    },
    cartedProductsCreate: function () {
      axios
        .post("/carted_products", this.cartedProductParams)
        .then((response) => {
          console.log(response, "HI");
          this.$route.push("products");
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ product.name }}</h1>
    <img v-bind:src="`${product.primary_image}`" />
    <p>{{ product.description }}</p>
    <p>Price: ${{ product.price }}</p>
    <button v-on:click="cartedProductsCreate()">Add To Cart</button>
  </div>
</template>

<style></style>
