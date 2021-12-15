<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <ul>
      <div v-for="error in errors" v-bind:key="error">{{ error }}</div>
    </ul>
    <div v-for="choice in choices">
      <img :src="`https://image.tmdb.org/t/p/w500/${choice[0].poster_path}`">
      <p>title: {{ choice[0].title || choice[0].original_name }} </p>
      <p>Rating Average: {{ choice[0].vote_average  }}/10 ({{ choice[0].vote_count }} votes)</p>
      <p>description: {{ choice[0].overview }} </p>
      <button v-on:click="removeMovie(choice)">Eliminate Option</button>
      <br />
      <a :href="`${choice[0].urls[0].web_url}`"><button>Link</button></a>
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
        source_ids: [],
        movies: [],
        currentMovie: {},
        errors: [],
        urls: [],
      };
    },
    // mounted() {
    //   if (localStorage.source_ids) {
    //     this.source_ids = localStorage.source_ids;
    //   }
    // },
    created: function () {
      this.choicesIndex();
      // setTimeout(() => { this.photosIndex() }, 2000);
      // setTimeout(() => { this.urlsIndex() }, 2000);
    },
    methods: {
      choicesIndex: function () {
        console.log('in choices index')
        axios.get("/choices").then(response => {
          console.log(response.data)
          this.choices = response.data;
        })
        .catch((error) => {
            console.log(error.response);
            this.errors = ["User must be logged in to use this service."];
        })
      },
      // photosIndex: function () {
      //   console.log('in photos index')
      //   for (let i = 0; i < this.choices.length; i++) {
      //     axios.get(`/photos/${this.choices[i]['tmdb_id']}?tmdb_type=${this.choices[i]['tmdb_type']}`).then(response => {
      //       this.movies.push(response.data)
      //     });
      //   }
      // },
      // urlsIndex: function () {
      //   console.log('in urls index')
      //   for (let i = 0; i < this.choices.length; i++) {
      //     axios.get(`/urls/${this.choices[i]['id']}`).then(response => {
      //       console.log(response.data);
      //       this.urls.push(response.data)
      //     });

      //   }
      // },
      removeMovie: function (theChoice) {
        console.log('in the movie eliminator')
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