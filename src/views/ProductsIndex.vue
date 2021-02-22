<template>
  <div class="index">
    <h1>All Products</h1>
    <div v-for="product in products" v-bind:key="product.id">
      <h2>{{ product.name }}</h2>
      <p>{{ product.price }}</p>
      <p>{{ product.description }}</p>
      <img v-bind:src="product.primary_image_url" alt="" />
      <router-link v-bind:to="`/products/${product.id}/edit`">Edit Product</router-link>
      <button v-on:click="destoryProduct(product)">Destroy product</button>
      <router-link to="/products">Back to all Products</router-link>
    </div>
  </div>
</template>

<style>
img {
  width: 250px;
}
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      products: [],
    };
  },
  created: function() {
    axios.get("/api/products").then(response => {
      console.log("products index", response);
      this.products = response.data;
    });
  },
  methods: {
    destroyProduct: function(product) {
      axios.delete("/api/products/" + product.id).then(response => {
        console.log("products destory", response);
        this.$router.push("/products");
      });
    },
  },
};
</script>
