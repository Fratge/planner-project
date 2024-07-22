<template>
  <NavBar></NavBar>
  <router-view/>
</template>


<script>
import NavBar from '@/components/NavBar.vue';

export default{
  components: { NavBar }
}
</script>

<style>
body{
  background-color: #1b1b1b;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  text-align: center;
  color: #555;
}

.main-nav {
    text-align: center;
    margin: 40px auto;
  }
  .main-nav a{
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: #999;
    font-size: 18px;
  }
  a.router-link-active {
    border-bottom: 2px solid #00ce89;
    padding-bottom: 4px;
  }
</style>
