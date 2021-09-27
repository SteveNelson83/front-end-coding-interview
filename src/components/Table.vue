<template>
  <table class="table">
    <tr>
      <th>Name</th>
      <th>User Name</th>
      <th>Email Address</th>
      <th>Phone Number</th>
      <th>Website</th>
    </tr>
    <tr v-for="(user) in users" :key="user.id">
      <td><input type="text" v-model="user.name" v-bind:disabled="user.disabled"/></td>
      <td><input type="text" v-model="user.username" v-bind:disabled="user.disabled"/></td>
      <td><input type="text" v-model="user.email" v-bind:disabled="user.disabled"/></td>
      <td><input type="text" v-model="user.phone" v-bind:disabled="user.disabled"/></td>
      <td><input type="text" v-model="user.website" v-bind:disabled="user.disabled"/></td>
      <button type="button" @click="user.disabled = !user.disabled">EDIT</button>
    </tr>
  </table>
</template>

<script>
  export default {
    data() {
      return {
        users: [],
        disabled: true
      };
    },

    methods: {
      async getData() {
        try {
          const response = await this.$http.get(
            "https://jsonplaceholder.typicode.com/users"
          );
          this.users = response.data.map(v => ({...v, disabled: true}));
          console.log(this.users);
        } catch (error) {
          console.log(error);
        }
      },
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
  
  table {
    background: blueviolet;
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