<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newProductParams: {},
      errors: [],
    };
  },
  created: function () {},
  methods: {
    productsCreate: function () {
      axios
        .post("/products", this.newProductParams)
        .then((response) => {
          console.log(response.data, "Product created");
          this.$router.push("/products");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          console.log(this.errors);
        });
    },
  },
};
</script>

<template>
  <div class="home">
    Name:
    <input v-model="newProductParams.name" />
    Description:
    <input v-model="newProductParams.description" />
    Supplier ID:
    <input v-model="newProductParams.supplier_id" />
    Price:
    <input v-model="newProductParams.price" />
    <!-- <input v-model="newProductParams.images" /> -->
    <button v-on:click="productsCreate()">Submit</button>
  </div>
</template>

<style></style>
