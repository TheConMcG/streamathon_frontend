<template>
    <!-- Wrapper -->
  <div id="wrapper" class="fade-in">

    <router-view />

    <!-- Copyright -->
    <div id="copyright">
      <ul>
        <li>&copy; Untitled</li>
        <li>Design: <a href="https://html5up.net">HTML5 UP</a></li>
        <li> {{ isLoggedIn() }} </li>
      </ul>
    </div>

  </div>
</template>

<style>

</style>

<script>
  export default {
    methods: {
      isLoggedIn: function() {
        if (localStorage.getItem('jwt')) {
          return true;
        } else {
          return false;
        }
      }
    }
  }
</script>

