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
            <td>{{user.name}}</td>
            <td>{{user.username}}</td>
            <td>{{user.emailaddress}}</td>
            <td>{{user.phone}}</td>
            <td>{{user.website}}</td>
        </tr>
    </table>
</template>

<script>
export default {
  data() {
    return {
      users: [],
    };
  },

  methods: {
    async getData() {
      try {
        const response = await this.$http.get(
          "https://jsonplaceholder.typicode.com/users"
        );
        this.users = response.data;
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
</style>