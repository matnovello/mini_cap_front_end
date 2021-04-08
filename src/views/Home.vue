<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="login">click to login</button>
    <button v-on:click="productsIndex">Click For Index </button>

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
    };
  },
  created: function () {},
  methods: {
    login: function () {
      var params = {
        email: "swag@gmail.com",
        password: "password",
      };
      axios
        .post("/api/sessions", params)
        .then((response) => {
          axios.defaults.headers.common["Authorization"] = "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
        })
        .catch((error) => {
          console.log(error.response);
          this.errors = ["Invalid email or password."];
          this.email = "";
          this.password = "";
        });
    },
    productsIndex: function () {
      axios.get("/api/products").then((response) => {
        console.log(response.data);
      });
    },
  },
};
</script>