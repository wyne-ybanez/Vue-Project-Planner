<template>
  <Navbar />
  <!-- Router view automatically picks Home, referenced in router folder -->
  <router-view/>
</template>

<script>
// Import for reference
import Navbar from './components/Navbar.vue'

// Export to register ie. register what component you're going to use in this component
export default {
  components: { Navbar }
}
</script>

<style>
body {
  background: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  color: #555;
}
</style>
