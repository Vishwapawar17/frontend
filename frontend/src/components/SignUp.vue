<template>
  <div>
    <form class="register" @submit="onSubmit">
      <img class="logo" src="../assets/EMS.png" alt="Logo" />
      <h2>Sign Up/Register </h2>
      <input required type="text" v-model="name" placeholder="Your Name" />
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
      <button class="btn">Sign Up</button>
       <div>
          Already have an account? <router-link to="/login">Login</router-link>
      </div>
    </form>
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
  
    async onSubmit(e) {
      e.preventDefault();
      const userData = {
        name: this.name,
        email: this.email,
        id: Math.floor(Math.random() * 100000),
        password: this.password,
      };
      let result = await axios.post("http://localhost:8080/admin/register", userData);
      if (result.status == 200) {
      localStorage.setItem("user-info",JSON.stringify(result.data))
      this.$router.push({name:"Login"})
      }
      (this.name = ""), (this.email = ""), (this.password = "");
    },
  },
  mounted(){
    let user = localStorage.getItem("user-info");
    if(user){
      this.$router.push({name:"Login"})
    }
  }
};
</script>

<style scoped>
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