<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <form v-on:submit.prevent="submit()">
      <h1><button v-on:click="submit1">Login</button></h1>
      <h1><button v-on:click="submit2">Set Streaming Sites</button></h1>
      <h1><button v-on:click="submit3">Logout</button></h1>
    </form>
  </div>
</template>

<style></style>

<script>
  export default {
    data: function () {
      return {
        message: "Manage Account",
      };
    },
    created: function () {},
    methods: {
      submit1: function () {
        this.$router.push("/login");
      },
      submit2: function () {
        this.$router.push("/services/new");
      },
      submit3: function () {
        this.$router.push("/logout");
      }
    },
  };
</script>