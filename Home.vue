<template>
  <Header />
  <!-- <Add @on_new_add="addTodo"/> -->
  <h2 class="resthed">List of Restaurants</h2>
  <table border="1" class="sthome">
    <td style="text-align: center">ID</td>
    <td style="text-align: center">NAME</td>
    <td style="text-align: center">ADDRESS</td>
    <td style="text-align: center">CONTACT</td>
    <td style="text-align: center">Status</td>

    <tr v-for="item in restaurants" :key="item.id">
      <td style="text-align: center">{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.address }}</td>
      <td>{{ item.contact }}</td>
      <td style="text-align: center">
        <router-link :to="'/update/' + item.id">Update</router-link>
      </td>
    </tr>
  </table>
</template>

<script>
import Header from "./Header.vue";
// import Add from './Add.vue'
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      name: "",
      restaurants: [],
    };
  },
  components: {
    Header,
    //    Add,
  },
  // data(){
  //     return{
  //         restaurants:{}
  //     }
  // },
  // methods: {
  //     addTodo(item) {

  //         this.restaurants=item
  //     }
  // },

  async mounted() {
    let newuser = localStorage.getItem("user-info");
    console.log("aaa", newuser);

    this.name = JSON.parse(newuser).name;
    if (!newuser) {
      this.$router.push({ name: "SignUp" });
    }
    let result = await axios.get("http://localhost:3000/restaurants");
    console.warn(result);

    this.restaurants = result.data;
  },
};
</script>

<style scoped>
.sthome {
  width: 500px;
  height: 200px;
}

.style {
  text-align: center;
}
</style>

