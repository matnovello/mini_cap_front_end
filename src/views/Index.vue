<template>
  <div class="index">
    <h1>{{ message }}</h1>
    <div class="row">
  <div class="col-sm-6" v-for=" product in products">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">{{ product.name }} </h5>
        <p class="card-text">{{ product.description }} </p>
        <img style="width: 200px" v-bind:src="product.image_url" class="card-img-top" alt="...">
        <a href="#" class="btn btn-primary">More Info</a>
      </div>
    </div>
  </div>
</div>

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
      email: "",
      password: "",
      products: {},
    };
  },
  created: function () {
    this.productsIndex();
  },
  methods: {
    productsIndex: function () {
      axios.get("/api/products").then((response) => {
        console.log(response.data);
        this.products = response.data;
      });
    },
  },
};
</script>