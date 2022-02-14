<template>
  <nav>
    <div class="nav-title">
      <router-link class="link" to="/">
        <h2>MOVIES <span>APP</span></h2>
      </router-link>
    </div>
  </nav>
</template>

<script>
export default {
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  nav {
    display: flex;
    justify-content: center;
    background: #333;
    color: #ddd;
    padding: 20px 60px;
  }

  .nav-title span {
    color: rgb(255, 39, 39);
  }
</style>
