<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <input type="checkbox" id="netflix" value="203" v-model="checkedServices">
      <label for="netflix">Netflix</label>
      <input type="checkbox" id="hulu" value="157" v-model="checkedServices">
      <label for="hulu">Hulu</label>
      <input type="checkbox" id="amazonPrime" value="26" v-model="checkedServices">
      <label for="amazonPrime">Amazon Prime</label>
      <input type="checkbox" id="hboMax" value="387" v-model="checkedServices">
      <label for="hboMax">HBO Max</label>
      <input type="checkbox" id="disney+" value="372" v-model="checkedServices">
      <label for="Disney+">Disney+</label>
      <input type="checkbox" id="peacock" value="388" v-model="checkedServices">
      <label for="peacock">Peacock</label>
      <br>
      
      <span>Checked Services: {{ checkedServices }}</span>
      <br />
      <input type="submit" value="Submit" />
    </form>
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
            this.$router.push("/choices");
          })
          .catch((error) => {
            this.errors = error.response.data.errors;
          });
      }
    }
  };
</script>