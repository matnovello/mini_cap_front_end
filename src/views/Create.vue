<template>
  <div class="create">
    <h1>{{ message }}</h1>
    <form v-on:submit.prevent="productCreate()">
      <h1>Login</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Name:</label>
        <input type="text" class="form-control" v-model="name">
      </div>
      <div class="form-group">
        <label>Price:</label>
        <input type="text" class="form-control" v-model="price">
      </div>
      <div class="form-group">
        <label>Description:</label>
        <input type="text" class="form-control" v-model="description">
      </div>
      <div class="form-group">
        <label>Supplier ID:</label>
        <input type="text" class="form-control" v-model="supplier_id">
      </div>
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      errors: {},
      name: "",
      price: "",
      description: "",
      supplier_id: "",
    };
  },
  created: function () {},
  methods: {
    productCreate: function () {
      var params = {
        name: this.name,
        price: this.price,
        description: this.description,
        supplier_id: this.supplier_id,
      };
      axios.post("http://localhost:3000/api/products/create", params).then((response) => {
        console.log(response.data);
        // $this.router.push("/show")
      });
    },
  },
};
</script>