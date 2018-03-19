<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>

html {
  background-color: #eee;
}

body {
  margin: 0 auto;
  padding: 0;
  max-width: 1200px;
  background: white;
  box-shadow: 0px 2px 28px -8px rgba(0,0,0,0.75);
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
