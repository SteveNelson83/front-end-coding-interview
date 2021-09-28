<template>
  <div>
  <h1>CURRENT USERS</h1>
  <table class="table">
    <tr>
      <th>Name</th>
      <th>User Name</th>
      <th>Email Address</th>
      <th>Phone Number</th>
      <th>Website</th>
    </tr>
    <tr v-for="(user) in users" :key="user.id">
      <td><input :class="'user'+user.id" type="text" v-model="user.name" v-bind:disabled="user.disabled"/></td>
      <td><input :class="'user'+user.id" type="text" v-model="user.username" v-bind:disabled="user.disabled"/></td>
      <td><input :class="'user'+user.id" type="text" v-model="user.email" v-bind:disabled="user.disabled"/></td>
      <td><input :class="'user'+user.id" type="text" v-model="user.phone" v-bind:disabled="user.disabled"/></td>
      <td><input :class="'user'+user.id" type="text" v-model="user.website" v-bind:disabled="user.disabled"/></td>
      <button type="button" @click="user.disabled = !user.disabled">EDIT</button>
      <button type="button" @click="saveUser(user)">SAVE</button>
    </tr>
  </table>
    <h1>ADD USER</h1>
    <form id="signup-form" @submit.prevent="addUser">
      <input type="text" v-model="name" placeholder="name"/>
      <input type="text" v-model="username" placeholder="username"/>
      <input type="text" v-model="email" placeholder="email"/>
      <input type="text" v-model="phone" placeholder="phone"/>
      <input type="text" v-model="website" placeholder="website"/>
      <button type="submit" >ADD</button>
    </form>
  </div>
</template>

<script>
  import axios from 'axios';
  export default {
    data() {
      return {
        users: [],
        name: '',
        username: '',
        email: '',
        phone: '',
        website: '',
        numberOfUsers: 0
      };
    },

    methods: {
      async getData() {
        try {
          const response = await axios.get(
            "https://jsonplaceholder.typicode.com/users"
          );
          this.users = response.data.map(v => ({...v, disabled: true}));
          this.numberOfUsers = this.users.length;
          console.log(this.users);
        } catch (error) {
          console.log(error);
        }
      },
      
      async saveUser(user) {
        const updatedUserData = Array.from(document.querySelectorAll('.user' + user.id), ({ value }) => value);
        console.log(updatedUserData);

        const response = await axios.put("https://jsonplaceholder.typicode.com/users/"+user.id, 
        {
          name: updatedUserData[0],
          username: updatedUserData[1],
          email: updatedUserData[2],
          phone: updatedUserData[3],
          website: updatedUserData[4],
        });
        console.log(response.data);
      },
      
      async addUser() {
        console.log({ name: this.name, email: this.email });
        const response = await axios.post("https://jsonplaceholder.typicode.com/users/", 
        {
          id: this.numberOfUsers+1,
          name: this.name,
          username: this.username,
          email: this.email,
          phone: this.phone,
          website: this.website,
        });
        console.log(response);
      }
    },
    created() {
      this.getData();
    },
  };
</script>

<style>
  table,
  th,
  td {
    border: 1px solid;
  }
  
  th,
  td {
    background: white;
  }
  input:disabled {
    background: black;
    color: white;
  }
  input:enabled {
    background: white;
    color: black;
  }
</style>