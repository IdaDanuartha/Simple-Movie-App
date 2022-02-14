<template>
  <div>
    <Navbar></Navbar>
  </div>
  <router-view />
</template>

<script>
import Navbar from './components/Navbar.vue'

export default {
  name: "App",
  components: {
    Navbar,
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  color: #ddd;
  font-family: 'Courier New', Courier, monospace;
}

body {
  background: #222;
  overflow-x: hidden;
}

.container {
  max-width: 1000px;
  margin: 20px auto 100px;
}

.link {
    text-decoration: none;
    color: #ddd;
}
</style>