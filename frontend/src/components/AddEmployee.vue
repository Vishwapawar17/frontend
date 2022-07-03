<template>
  <Header />
  <div class="restraunt-container">
    <form class="register" @submit="onSubmit">
      <h2>Add New Employee</h2>
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
      <button class="btn btn-primary">Add Employee</button>
    </form>

     

  </div>
</template>

<script>
import axios from "axios";
import Header from "./Header";
export default {
  name: "Add",
  components: { Header },
  data() {
    return {
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
     async onSubmit(e) {
      e.preventDefault();
      let self = this;
      //console.log(this.employee)
       await axios.post(
        "http://localhost:8081/api/employee/addCustomer",
        this.employee
      ).then((res)=>{
        console.log(res.data)
        alert("added successfully")
        self.$router.push("/");
      }).catch((err)=>{
        console.log(err)
      })
    },
  }
  
};
</script>

<style>
.restraunt-container {
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