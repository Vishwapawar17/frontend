<template>
  <Header />
  <div class="restaurant-container">
    <form class="register" @submit="onSubmit">
      <h2>Edit Employee</h2>
      <input
        required
        type="text"
        v-model="employee.name"
        placeholder="Employee's Name"
      />
      <input
        required
        type="text"
        v-model="employee.address"
        placeholder="Employee's Address"
      />
      <input
        required
        type="number"
        v-model="employee.mobile"
        placeholder="Employee's Mobile Number"
      />
      <input
        required
        type="email"
        v-model="employee.email"
        placeholder="Employee's Email "
      />
      <input
        required
        type="password"
        v-model="employee.password"
        placeholder="Employee's Password"
      />
      <button class="btn btn-warning" @click="getId">Update</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
import Header from "./Header";
export default {
  name: "Update",
  components: { Header },
  data() {
    return {
      employees: [],
      employee: {
        name: "",
        address: "",
        mobile: "",
        email: "",
        password: "",
      },
      show: true,
    };
  },
  methods: {
    onSubmit(e) {
      const path = window.location.pathname;
      const segments = path.split("/");
      // console.log(path);
      const editId = segments[2];
      console.log(editId);
      //  console.log(this.$route.params)
      e.preventDefault();
      let apiUrl = `http://localhost:8080/api/employee/updateEmployee/${editId}`;
      axios
        .put(apiUrl, this.employee)
        .then(() => {
          location.reload();
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style>
.restaurant-container {
  margin-top: 30px;
}
.logo {
  width: 150px;
  height: 150px;
}
.register {
  width: 30vw;
  display: block;
  margin: 0 auto;
  padding: 20px;
  border: 2px solid rgb(51, 77, 160);
  border-radius: 10px;
  font-size: 20px;
}
.register input {
  height: 40px;
  width: 280px;
  display: block;
  padding-left: 30px;
  margin: 0px auto 30px auto;
  border: 2px solid rgb(51, 77, 160);
  border-radius: 5px;
}
.btn {
  height: 44px;
  width: 317px;
  margin-bottom: 30px;
  border: 1px solid rgb(0, 30, 128);
  background: rgb(0, 30, 128);
  color: white;
  text-transform: uppercase;
  font-weight: 900;
  font-size: 18px;
  border-radius: 5px;
  cursor: pointer;
}
.btn:hover {
  transform: scale(1.1);
}
</style>
