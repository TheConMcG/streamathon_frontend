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
      <div class="login">
        <form method="post" v-on:submit.prevent="submit()">
          <h1>Login</h1>
          <ul>
            <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
          </ul>
          <div>
            <label>Email:</label>
            <input type="email" placeholder="email@example.com" v-model="newSessionParams.email" />
          </div>
          <br />
          <div>
            <label>Password:</label>
            <input type="password" placeholder="password" v-model="newSessionParams.password" />
          </div>
          <br />
          <input type="submit" value="Submit" />
        </form>
      </div>
		</div>
	</div>
</template>
  



<script>
  import axios from "axios";

  export default {
    data: function () {
      return {
        newSessionParams: {},
        errors: []
      };
    },
    methods: {
      submit: function () {
        axios
          .post("/sessions", this.newSessionParams)
          .then((response) => {
            axios.defaults.headers.common["Authorization"] =
              "Bearer " + response.data.jwt;
            localStorage.setItem("jwt", response.data.jwt);
            this.$router.push("/");
          })
          .catch((error) => {
            console.log(error.response);
            this.errors = ["Invalid email or password."];
            this.email = "";
            this.password = "";
          });
      }
    }
  };
</script>
