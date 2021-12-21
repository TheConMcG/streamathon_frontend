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
		</nav>
		<!-- Main -->
		<div id="main">
      <h2>Please select the streaming services you currently have subscriptions to:</h2>
      <div class="signup">
        <form v-on:submit.prevent="submit()">
          <input type="checkbox" id="hulu" value="157" v-model="checkedServices">
          <label for="hulu"><img src="/images/hulu.png" /></label>
          <input type="checkbox" id="netflix" value="203" v-model="checkedServices">
          <label for="netflix"><img src="/images/netflix.png" /></label>
          <input type="checkbox" id="disney+" value="372" v-model="checkedServices">
          <label for="disney+"><img src="/images/disneyplus.png" /></label>
          <input type="checkbox" id="hboMax" value="387" v-model="checkedServices">
          <label for="hboMax"><img src="/images/hbomax.png" /></label>
          <input type="checkbox" id="amazonPrime" value="26" v-model="checkedServices">
          <label for="amazonPrime"><img src="/images/prime.png" /></label>
          <input type="checkbox" id="peacock" value="388" v-model="checkedServices">
          <label for="peacock"><img src="/images/peacock.png" /></label>
          <br>
          <span>Checked Services: {{ checkedServices }}</span>
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
        newServiceParams: {},
        checkedServices: [],
        errors: []
      };
    },
    created: function () {},
    methods: {
      submit: function () {
        axios
          .post("/service_users", {service_ids: this.checkedServices})
          .then((response) => {
            console.log(response.data);
            this.$router.push("/");
          })
          .catch((error) => {
            this.errors = error.response.data.errors;
          });
      }
    }
  };
</script>