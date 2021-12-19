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
      <div class="signup">
        <form v-on:submit.prevent="submit()">
          <h1>Signup</h1>
          <ul>
            <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
          </ul>
          <div>
            <label>Name:</label>
            <input type="text" v-model="newUserParams.name" />
          </div><br />
          <div>
            <label>Email:</label>
            <input type="email" v-model="newUserParams.email" />
          </div><br />
          <div>
            <label>Password:</label>
            <input type="password" v-model="newUserParams.password" />
          </div><br />
          <div>
            <label>Password confirmation:</label>
            <input type="password" v-model="newUserParams.password_confirmation" />
          </div><br />
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
        newUserParams: {
          name: "tester13",
          email: "tester13@tester.com",
          password: "password",
          password_confirmation: "password"
        },
        newSessionParams: {},
        errors: []
      };
    },
    methods: {
      submit: function () {
        axios
          .post("/users", this.newUserParams)
          .then((response) => {
            console.log(response.data);
            // debugger;
            axios.defaults.headers.common["Authorization"] =
              "Bearer " + response.data.jwt;
            localStorage.setItem("jwt", response.data.jwt);
            this.$router.push("/services/new");
          })
          .catch((error) => {
            this.errors = error.response.data.errors;
          });
      }
    }
  };
</script>