<template>
  <div class="nav">
    <a href="/">Home</a>
    <a href="/add">Add</a>
  
    <a href="/signup">Sign Up</a>
    <a href="/login">Login</a>
    <a href="#" v-on:click="logout">Logout</a>
  </div>
</template>

<script>
export default {
  name: "Header",
  methods: {
    logout() {
      localStorage.clear();
      this.$router.push({ name: "Login" });
    },
  },
};
</script>

<style scoped>
.nav {
  background-color: rgb(0, 30, 128);
  overflow: hidden;
}
.nav a {
  float: left;
  color: white;
  text-align: center;
  padding: 10px 74px;
  text-decoration: none;
  font-size: 16px;
  margin: 0px auto 0px auto;
  font-size: 18px;
  font-weight: 700;
}
.nav a:hover {
  transform: scale(1.3);
  text-decoration: underline;
  background-color: rgb(29, 53, 134);
  color: white;
}
</style>