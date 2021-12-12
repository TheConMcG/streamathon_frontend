<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <ul>
      <div v-for="error in errors" v-bind:key="error">{{ error }}</div>
    </ul>
    <div v-for="movie in movies">
      <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`">
      <p>title: {{ movie.title || movie.original_name }} </p>
      <p>Rating Average: {{ movie.vote_average  }}/10 ({{ movie.vote_count }} votes)</p>
      <p>description: {{ movie.overview }} </p>
      <button v-on:click="removeMovie(movie)">Eliminate Option</button>
      <hr />
    </div>
  </div>
</template>

<style></style>

<script>
  import axios from 'axios'
  
  export default {
    data: function () {
      return {
        message: "Rules of the Game: you currently have five random options from across your streaming platforms. We take turn eliminating options until you're left with something to watch. Picking something has never been easier!",
        choices: {},
        movies: [],
        currentMovie: {},
        errors: [],
      };
    },
    created: function () {
      this.choicesIndex();
      setTimeout(() => { this.photosIndex() }, 2000);
    },
    methods: {
      choicesIndex: function () {
        console.log('in choices index')
        axios.get("/choices").then(response => {
          this.choices = response.data['titles'];
        })
        .catch((error) => {
            console.log(error.response);
            this.errors = ["User must be logged in to use this service."];
        })
      },
      photosIndex: function () {
        console.log('in photos index')
        for (let i = 0; i < this.choices.length; i++) {
          axios.get(`/photos/${this.choices[i]['tmdb_id']}?tmdb_type=${this.choices[i]['tmdb_type']}`).then(response => {
            this.movies.push(response.data)
          });
        }
      },
      removeMovie: function (theMovie) {
        console.log('in the movie eliminator')
        let i = this.movies.indexOf(theMovie)
        this.movies.splice(i, 1);
        if (this.movies.length === 4) {
          this.message = "My turn..."
          function getRandomInt(max) {
            return Math.floor(Math.random() * max);
          }
          let j = getRandomInt(4);
          setTimeout(() => { this.movies.splice(j, 1) }, 3000);
          setTimeout(() => { this.message="Your turn..." }, 4000);
        }
        else if (this.movies.length === 2) {
          this.message = "My turn..."
          function getRandomInt(max) {
            return Math.floor(Math.random() * max);
          }
          let j = getRandomInt(2);
          setTimeout(() => { this.movies.splice(j, 1) }, 3000);
          setTimeout(() => { this.message="Here's your final choice!" }, 3010);
        }
      }
    }
  }
</script>