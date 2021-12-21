<template>
  <div class="home">
    <!-- Intro -->
    <div id="intro">
      <h1>How To<br />
        Decide?</h1>
      <p>{{ message }}<br /></p>
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
      <section class="posts">
        <article v-for="choice in choices">
          <header>
            <h2><a href="#">{{ choice[0].title || choice[0].original_name }}</a></h2>
            <h4><a href="#">Rating Average: {{ choice[0].vote_average  }}/10 ({{ choice[0].vote_count }} votes)</a></h4>
          </header>
          <a href="#" class="image fit"><img :src="`https://image.tmdb.org/t/p/w500/${choice[0].poster_path}`" alt="" /></a>
          <h5>description: {{ choice[0].overview }} </h5>
          <ul class="actions special">
            <li><a href="#" class="button" v-on:click="removeMovie(choice)">Eliminate Option</a></li>
            <li><a :href="`${choice[0].urls[0].web_url}`" class="button">Watch Now!</a></li>
          </ul>
        </article>
      </section>
    </div>
  </div>
</template>

<style></style>

<script>
  import axios from 'axios'
  
  export default {
    data: function () {
      return {
        message: "You currently have options from across your streaming platforms. We take turns eliminating them until you're left with something to watch. Picking something has never been easier!",
        message2: "",
        choices: {},
        errors: [],
        choiceParams: {
          limit: this.$route.query.limit,
          genre: this.$route.query.genre,
          tmdb_type: this.$route.query.tmdb_type,
        },
      };
    },
    created: function () {
      this.choicesIndex();
    },
    methods: {
      choicesIndex: function () {
        axios.get(`/choices?limit=${this.choiceParams["limit"]}&genre=${this.choiceParams["genre"]}&tmdb_type=${this.choiceParams["tmdb_type"]}`).then(response => {
          console.log(response.data)
          this.choices = response.data;
        })
        .catch((error) => {
            console.log(error.response);
            this.errors = ["User must be logged in to use this service."];
        })
      },
      removeMovie: function (theChoice) {
        let i = this.choices.indexOf(theChoice)
        this.choices.splice(i, 1);
        if (this.choices.length === 4) {
          this.message = "My turn..."
          function getRandomInt(max) {
            return Math.floor(Math.random() * max);
          }
          let j = getRandomInt(4);
          setTimeout(() => { this.choices.splice(j, 1) }, 3000);
          setTimeout(() => { this.message="Your turn..." }, 4000);
        }
        else if (this.choices.length === 2) {
          this.message = "My turn..."
          function getRandomInt(max) {
            return Math.floor(Math.random() * max);
          }
          let j = getRandomInt(2);
          setTimeout(() => { this.choices.splice(j, 1) }, 3000);
          setTimeout(() => { this.message="Here's your final choice!" }, 3010);
        }
      }
    }
  }
</script>