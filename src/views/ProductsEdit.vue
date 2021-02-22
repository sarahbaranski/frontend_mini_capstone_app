<template>
  <div class="products-edit">
    <h1>Edit Product</h1>
    <form v-on:sumbit.prevent="updateProduct(product)">
      <ul>
        <li :v-for="error in errors">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="product.name" />
      Price:
      <input type="text" v-model="product.price" />
      Description:
      <input type="text" v-model="product.description" />
      Supplier Id:
      <input type="text" v-model="product.supplierId" />
      Image Url:
      <input type="text" v-model="product.image" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      product: {},
      erros: [],
    };
  },
  created: function() {
    axios.get("/api/products/" + this.$route.params.id).then(response => {
      console.log("products show", response);
      this.product = response.data;
    });
  },
  methods: {
    updateProduct: function(product) {
      var params = {
        name: product.name,
        price: product.price,
        description: product.description,
        supplier_id: product.supplierId,
        image_url: product.image,
      };
      axios.patch("/api/products/" + product.id, params).then(response => {
        console.log("products update", response);
        this.$router.push("/products");
      });
    },
  },
};
</script>
