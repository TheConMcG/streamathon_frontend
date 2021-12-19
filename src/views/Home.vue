<template>
  <div class="home">
    <!-- Intro -->
    <div id="intro">
      <h1>This is<br />
        Streamathon</h1>
      <p>A free & fun way to decide what to stream.<br />Spend more time watching & less time scrolling.</p>
      <ul class="actions">
        <li><a href="#nav" class="button icon solid solo fa-arrow-down scrolly">Continue</a></li>
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

      <!-- Featured Post -->
      <article class="post featured">
        <header class="major">
          <h2><a href="#">{{ message }}</a></h2>
          <p>
            <form v-on:submit.prevent="submit()">
              <h1><button v-if="$parent.isLoggedIn()"v-on:click="submit">What to watch?</button></h1>
              <router-link to="/login"><h1><button v-if="!$parent.isLoggedIn()">Login</button></h1></router-link>
            </form>
          </p>
        </header>
      </article>

    </div>
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