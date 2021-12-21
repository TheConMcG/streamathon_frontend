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
              <div class="col-12" v-if="$parent.isLoggedIn()">
                <select name="limit" id="limit" v-model="choiceParams.limit">
                  <option value="">- Number of options to choose from -</option>
                  <option value="1">1</option>
                  <option value="3">3</option>
                  <option value="5">5</option>
                  <option value="7">7</option>
                  <option value="9">9</option>
                  <option value="11">11</option>
                </select>
              </div>
              <div class="col-12" v-if="$parent.isLoggedIn()">
                <select name="genre" id="genre" v-model="choiceParams.genre">
                  <option value="">- Genre -</option>
                  <option value="1">Action</option>
                  <option value="33">Anime</option>
                  <option value="4">Comedy</option>
                  <option value="5">Crime</option>
                  <option value="6">Documentary</option>
                  <option value="7">Drama</option>
                  <option value="8">Family</option>
                  <option value="9">Fantasy</option>
                  <option value="11">Horror</option>
                  <option value="12">Mystery</option>
                  <option value="14">Romance</option>
                  <option value="40">Sci-Fi & Fantasy</option>
                  <option value="15">Science Fiction</option>
                  <option value="17">Thriller</option>
                  <option value="41">War & Politics</option>
                  <option value="19">Western</option>
                </select>
              </div>
              <div class="col-12" v-if="$parent.isLoggedIn()">
                <select name="type" id="type" v-model="choiceParams.tmdb_type">
                  <option value="">- Medium -</option>
                  <option value="movie">Movie</option>
                  <option value="short_film">Short Film</option>
                  <option value="tv_miniseries">TV Mini-Series</option>
                  <option value="tv_series">TV Show</option>
                  <option value="tv_special">TV Special</option>
                </select>
              </div>
              <h1><button v-if="$parent.isLoggedIn()" v-on:click="submit">What to watch?</button></h1>
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
        message: "Choose your game options!",
        errors: [],
        choiceParams: {
          limit: "",
          genre: "",
          tmdb_type: "",
        },
      };
    },
    created: function () {},
    methods: {
      submit: function () {
        this.$router.push(`/choices?limit=${this.choiceParams["limit"]}&genre=${this.choiceParams["genre"]}&tmdb_type=${this.choiceParams["tmdb_type"]}`); 
      }
    },
  };
</script>
