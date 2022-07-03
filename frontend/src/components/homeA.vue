<template>
  <Header />
  <h1>Welcome To Home Page</h1>
  <div class="table-div">
    <table class="">
      <tr>
        <!-- <td class="headers">Sr.No</td> -->
        <th class="headers">Name</th>
        <th class="headers">Mobile</th>
        <th class="headers">Address</th>
        <th class="headers">Email</th>
        <th class="headers">Action</th>
      </tr>
      <tr v-for="item in employees" :key="item._id">
        <!-- <td>{{ item._id }}</td> -->
        <td>{{ item.name }}</td>
        <td>{{ item.mobile }}</td>
        <td>{{ item.address }}</td>
        <td>{{ item.email }}</td>
        <!-- <td>{{ item.password }}</td> -->
        <td>
          <button class="btn-warning">
            <router-link :to="`/update/${item._id}`">Update</router-link>
          </button>

          &nbsp; &nbsp;
          <button class="btn-danger" v-on:click="deleteEmployee(item._id)">
            Delete
          </button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
import Header from "./Header";
import axios from "axios";
export default {
  name: "Home",
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
      editId: "",
    };
  },
  components: { Header },
  created() {
    let apiUrl = "http://localhost:8081/api/employee/getAll";
    axios
      .get(apiUrl)
      .then((res) => {
        this.employees = res.data.data.emp;
        console.log(res.data.data.emp);
      })
      .catch((error) => {
        console.log(error);
      });
  },
  methods: {
    deleteEmployee(id) {
      console.log(id);
      let apiUrl = `http://localhost:8080/api/employee/deleteById/${id}`;
      let indexOfEmployee = this.employees.findIndex(
        (element) => element.id === id
      );
      axios
        .delete(apiUrl)
        .then(() => {
          this.employees.splice(indexOfEmployee, 1);
         location.reload();
        })
        .catch((error) => {
          console.log(error);
        });
    },
    editEmployee(id) {
      this.editId = id;
    },
    handleEditEmployeeForm() {
      console.log(this.editemployee);
      let apiUrl = `http://localhost:8081/api/employee/updateById/${this.editId}`;
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

<style lang="css" scoped>
.table-div {
  display: flex;
  justify-content: center;
}
.headers {
  height: 50px;
  background-color: rgb(0, 30, 128);
  color: white;
}
td {
  width: 240px;
  height: 40px;
  font-size: 16px;
  font-weight: 700;
}
</style>