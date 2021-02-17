<template>
  <div class="create">
    <form v-on:submit.prevent="createProduct()">
      <h1>New Product</h1>
      <div>
        <router-link to="/login">Login</router-link>
      </div>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Name:</label>
        <input type="text" class="form-control" v-model="name" />
      </div>
      <div class="form-group">
        <label>Price:</label>
        <input type="text" class="form-control" v-model="price" />
      </div>
      <div class="form-group">
        <label>Description:</label>
        <input type="text" class="form-control" v-model="description" />
      </div>
      <div class="form-group">
        <label>Supplier:</label>
        <input type="text" class="form-control" v-model="supplierId" />
      </div>
      <div class="form-group">
        <label>Image:</label>
        <input type="text" class="form-control" v-model="image" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      name: "",
      price: "",
      description: "",
      supplierId: "",
      image: "",
      errors: [],
    };
  },
  methods: {
    createProduct: function() {
      var params = {
        name: this.name,
        price: this.price,
        description: this.description,
        supplier_id: this.supplierId,
        image_url: this.image,
      };
      axios
        .post("/api/products", params)
        .then(response => {
          console.log(response);
          this.$router.push("/products");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
