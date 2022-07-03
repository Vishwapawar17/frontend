<template>
  <div>
    <form class="register" @submit="onSubmit">
      <img class="logo" src="../assets/EMS.png" alt="Logo" />
      <h2>Login For Employee</h2>
      <input
        required
        type="email"
        v-model="email"
        placeholder="Your Email Id"
      />
      <input
        required
        type="password"
        v-model="password"
        placeholder="Your Password"
      />
      <button class="btn btn-primary">Login</button>
      <div>
        Are you a new user? <router-link to="/signup">Sign Up</router-link>
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    onSubmit(e) {
      let self = this;
      e.preventDefault();
      const userData = {
        email: this.email,
        password: this.password,
      };
      console.log(userData)
      // let result =  axios.post(
      //   `http://localhost:8080/admin/login`,userData
      // );
      let result  = axios.post(`http://localhost:8080/admin/login`, userData).then(function(response){
        console.log(response.data.status)
        if(response.data.status === "success"){
          self.$router.push({ name: "Home" });
        }
        else{
          alert("Please put valid email and password.");
        }
      }).catch(function(error){
        console.log(error)
      })
      console.log(result)
      // if (result.status == "success") {
      //   localStorage.setItem("user-info", JSON.stringify(result.data[0]));
       
      //   this.$router.push({ name: "Home" });
      // } else {
      //   //  console.log(localStorage.getItem("user-info"))
      //   alert("Please put valid email and password.");
      // }
      // (this.email = ""), (this.password = "");
    },
  }
};
</script>

<style>
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