<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <form v-on:submit.prevent="submit()">
      <h1><button v-on:click="submit">What to watch?</button></h1>
    </form>
  </div>
</template>

<style></style>

<script>
  export default {
    data: function () {
      return {
        message: "Welcome to Streamathon!",
        errors: []
      };
    },
    created: function () {},
    methods: {
      submit: function () {
        this.$router.push("/choices");
      }
    },
  };
</script>