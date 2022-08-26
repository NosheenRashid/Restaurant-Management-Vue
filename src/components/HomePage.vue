<template>
  <HeaderPart />
  <h1>Hello {{ name }}, Welcome On Home Page</h1>
  <table border="2px">
    <tr>
      <th>ID</th>
      <th>Name</th>
      <th>Address</th>
      <th>Contact</th>
      <th>Actions</th>
    </tr>
    <tr v-for="item in restaurant" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.address }}</td>
      <td>{{ item.contact }}</td>
      <td>
        <a @click="openUrl('/update/' + item.id)" href="javascript:;">Update</a>
        <button @click="deleteRest(item.id)">Delete</button>
      </td>
    </tr>
  </table>
</template>

<script>
import axios from "axios";
import HeaderPart from "./HeaderPart.vue";

export default {
  name: "HomePage",
  data() {
    return {
      name: "",
      restaurant: [],
    };
  },
  methods: {
    openUrl(route) {
      this.$router.push(route);
    },
    async deleteRest(id) {
      let result = await axios.delete("http://localhost:3000/restaurant/" + id);
      if (result.status == 200) {
        this.loadData();
      }
    },
    async loadData() {
      let user = localStorage.getItem("user-info");
      this.name = JSON.parse(user).name;
      if (!user) {
        this.$router.push({ name: "SignUp" });
      }
      let result = await axios.get("http://localhost:3000/restaurant");
      console.log(result);
      this.restaurant = result.data;
    },
  },
  components: {
    HeaderPart,
  },
  mounted() {
    this.loadData();
  },
};
</script>
<style>
td,
tr {
  width: 160px;
  height: 60px;
}
</style>
