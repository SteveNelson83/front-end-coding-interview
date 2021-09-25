<template>
    <table></table>
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