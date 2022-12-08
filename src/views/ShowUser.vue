<script >

import axios from "axios";
const URL="http://localhost:3000/users";
export default {
  name: "adduser",
  data() {
    return {
      users: [],
      user: {},
      email: '',
      name: ''
    };
  },
  methods: {
    async getUsers() {
      try {
        const users = await axios.get(
          "http://localhost:3000/users"
        );

        this.users = users.data;
      } catch (e) {
        console.log(e);
      }
    },

    async storeUser() {
      try {
        const user = await axios.post(
          "http://localhost:3000/users", { name: this.name, email: this.email }
        );

        console.log(user)
      } catch (e) {
        console.log(e);
      }
    },

    async updateUser() {
      try {
        const user = await axios.put(
          "http://localhost:3000/users/" + this.user.id,
          {
            name: this.user.name,
            email: this.user.email,
          }
        );

        console.log(user.data);
        alert("User updated!");
      } catch (e) {
        console.log(e);
      }
    },

    async editUser(user) {
      this.user.name = user.name;
      this.user.email = user.email;
      this.user.id = user.id;
    },

    async deleteUser(id) {
      let x = window.confirm("You want to delete the user?");

      if (x) {
        const user = await axios.delete(
          "http://localhost:3000/users/" + id
        );

        console.log(user);
        alert("User deleted!");
      }
    },
  },
};



</script>

<template>
     <div>
    <button @click="getUsers">Get users</button> <br />
    
    <table border="1">
      
      <tr>
        <td>nom</td>
        <td>email</td>
      </tr>
      <tr class="users" v-for="user in users" :key="user.id">
       
        <td>{{ user.name }}</td>
        <td>{{ user.email }}</td>

        <td><button @click="editUser(user)"><RouterLink to="/edituser" class="nav-link">Edit</RouterLink></button></td>
        <td><button @click="deleteUser(user.id)">Delete</button></td>

      </tr>
  
  </table>
</div>



  </template>