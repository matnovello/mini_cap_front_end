<template>
  <div class="login">
    <h1>{{ message }}</h1>
    <form v-on:submit.prevent="login()">
      <h1>Login</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Email:</label>
        <input type="email" class="form-control" v-model="email">
      </div>
      <div class="form-group">
        <label>Password:</label>
        <input type="password" class="form-control" v-model="password">
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
      email: "",
      password: "",
      errors: {},
    };
  },
  created: function () {},
  methods: {
    login: function () {
      var params = {
        email: this.email,
        password: this.password,
      };
      axios.post("/api/sessions", params).then((response) => {
        axios.defaults.headers.common["Authorization"] = "Bearer " + response.data.jwt;
        localStorage.setItem("jwt", response.data.jwt);
        console.log(response.data.jwt);
      });
    },
  },
};
</script>