<template>
  <HeaderPart />
  <h1>Add Resturant</h1>
  <form class="add" action="">
    <input type="text" placeholder="Enter Name" v-model="restaurant.name" />
    <input
      type="address"
      placeholder="Enter Address"
      v-model="restaurant.address"
    />
    <input
      type="contact"
      placeholder="Enter Contact"
      v-model="restaurant.contact"
    />
    <button type="button" @click="addRest">Add New Resturant</button>
  </form>
</template>

<script>
import HeaderPart from "./HeaderPart.vue";
export default {
  name: "AddRest",
  data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  components: {
    HeaderPart,
  },
  methods: {
    addRest() {
      console.log(this.restaurant);
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>
<style>
.add input {
  width: 300px;
  height: 40px;
  padding-left: 30px;
  display: block;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
  border: 1px solid skyblue;
}
.add button {
  height: 40px;
  width: 300px;
  color: white;
  /* font-size: 15px; */
  background-color: skyblue;
  border: 1px solid skyblue;
}
.add button:hover {
  background-color: powderblue;
}
</style>
