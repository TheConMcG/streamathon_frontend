<template>
  <div class="home">
    <!-- Intro -->
    <div id="intro">
      <h1>This is<br />
        Streamathon</h1>
      <p>A free & fun way to decide what to stream.<br />Spend more time watching & less time scrolling.</p>
      <ul class="actions">
        <li><a href="#main" class="button icon solid solo fa-arrow-down scrolly">Continue</a></li>
      </ul>
    </div>
    <!-- Nav -->
    <nav id="nav">
      <ul class="links">
        <li class="active"><a href="/">Streamathon</a></li>
        <li v-if="!$parent.isLoggedIn()"><a href="/signup">Signup</a></li>
        <li><a href="/account">Account</a></li>
      </ul>
    </nav>
    <!-- Main -->
    <div id="main">
      <h1>{{ message }}</h1>
      <form v-on:submit.prevent="submit()">
        <h1><button v-if="!$parent.isLoggedIn()" v-on:click="submit1">Login</button></h1>
        <h1><button v-if="$parent.isLoggedIn()" v-on:click="submit2">Set Streaming Sites</button></h1>
        <h1><button v-if="$parent.isLoggedIn()" v-on:click="submit3">Logout</button></h1>
        <h1><button v-if="!$parent.isLoggedIn()" v-on:click="submit4">Signup</button></h1>
      </form>
    </div>
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
      },
      submit4: function () {
        this.$router.push("/signup");
      }
    },
  };
</script>