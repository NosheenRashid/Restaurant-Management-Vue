<template>
  <img class="logo" src="../assets/rest-logo.jpg" alt="" />
  <h1>SignUp</h1>
  <div class="register">
    <input type="text" placeholder="Enter Name" v-model="name" required />
    <input type="email" placeholder="Enter Email" v-model="email" required />
    <input
      type="password"
      placeholder="Enter Password"
      v-model="password"
      required
    />
    <button @click="signUp" class="btn">SignUp</button>
    <p>
      <router-link to="/login"> Login</router-link>
    </p>
  </div>
</template>
<script>
import axios from "axios";

export default {
  name: "SignUp",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async signUp() {
      console.log("signUp", this.name, this.email, this.password);
      let result = await axios.post(
        "http://localhost:3000/users",
        { withCredentials: true },
        {
          name: this.name,
          email: this.email,
          password: this.password,
        }
      );
      console.log(result);
      if (result.status == 201) {
        localStorage.setItem("user-info", JSON.stringify(result.data));
        this.$router.push({ name: "HomePage" });
      }
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
.register input {
  width: 300px;
  height: 40px;
  padding-left: 30px;
  display: block;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
  border: 1px solid skyblue;
}
.register button {
  height: 40px;
  width: 340px;
  color: white;
  /* font-size: 15px; */
  background-color: skyblue;
  border: 1px solid skyblue;
}
.btn:hover {
  background-color: powderblue;
}
</style>
