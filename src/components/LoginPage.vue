<template>
  <img class="logo" src="../assets/rest-logo.jpg" alt="" />
  <h1>Login</h1>
  <div class="login">
    <input type="email" placeholder="Enter Email" v-model="email" required />
    <input
      type="password"
      placeholder="Enter Password"
      v-model="password"
      required
    />
    <button @click="login" class="btn">Login</button>

    <p>
      <router-link to="/sign-up"> SignUp</router-link>
    </p>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "LoginPage",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}&password=${this.password}`
      );
      console.log(result);
      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "HomePage" });
      }
      console.log(result);
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "HomePage" });
    }
  },
};
</script>
<style>
.logo {
  width: 200px;
}
.login input {
  width: 300px;
  height: 40px;
  padding-left: 30px;
  display: block;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
  border: 1px solid skyblue;
}
.login button {
  height: 40px;
  width: 300px;
  color: white;
  /* font-size: 15px; */
  background-color: skyblue;
  border: 1px solid skyblue;
}
.btn:hover {
  background-color: powderblue;
}
p {
  margin-top: 10px;
}
</style>
