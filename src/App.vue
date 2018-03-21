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
  background-color: #555;
}

body {
  margin: 0 auto;
  padding: 0;
  max-width: 1200px;
  background: white;
  box-shadow: 0px 2px 28px -8px rgba(0,0,0,0.95);
}

#app, input, button {
  font-family: 'Roboto Mono', 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

h1 {
  color: #de3800;
}
</style>
