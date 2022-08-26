<template>
  <div class="nav">
    <a @click="openUrl('/')" href="javascript:;">Home</a>
    <a @click="openUrl('/add')" href="javascript:;">Add Restaurant</a>
    <!-- <a @click="openUrl('/update')" href="javascript:;">Update Restaurant</a> -->
    <a @click="logout" href="#">Logout</a>
  </div>
</template>
<script>
export default {
  name: "HeaderPart",
  methods: {
    openUrl(route) {
      this.$router.push(route);
    },
    logout() {
      localStorage.clear();
      this.$router.push({ name: "LoginPage" });
    },
  },
};
</script>
<style>
.nav {
  background-color: #333;
  overflow: hidden;
}
.nav a {
  float: left;
  color: #f2f2f2;
  text-align: center;
  padding: 10px 14px;
  text-decoration: none;
  font-size: 16px;
}
.nav a:hover {
  background-color: #ddd;
  color: #222;
}
</style>
