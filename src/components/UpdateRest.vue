<template>
  <HeaderPart />
  <h1>Update Resturant</h1>
  <form class="add" action="">
    <input type="text" placeholder="Enter Name" v-model="updateRest.name" />
    <input
      type="address"
      placeholder="Enter Address"
      v-model="updateRest.address"
    />
    <input
      type="contact"
      placeholder="Enter Contact"
      v-model="updateRest.contact"
    />
    <button type="button" @click="updateResto">Update Resturant</button>
  </form>
</template>

<script>
import HeaderPart from "./HeaderPart.vue";
import axios from "axios";
export default {
  name: "UpdateRest",
  data() {
    return {
      updateRest: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  methods: {
    async updateResto() {
      let result = await axios.put(
        "http://localhost:3000/restaurant/" + this.$route.params.id,
        // { withCredentials: true },
        {
          name: this.updateRest.name,
          address: this.updateRest.address,
          contact: this.updateRest.contact,
        }
      );
      console.log(result);
      if (result.status == 200) {
        this.$router.push({ name: "HomePage" });
      }
    },
  },
  components: {
    HeaderPart,
  },
  async mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
    let result = await axios.get(
      "http://localhost:3000/restaurant/" + this.$route.params.id
    );
    // console.log(this.$route.params.id);
    // console.log(result.data);
    this.updateRest = result.data;
  },
};
</script>
