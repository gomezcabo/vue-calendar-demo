<!-- PLANTILLA -->
<template lang="jade">
div
  p {{ greeting }} World
</template>

<!-- LÓGICA / INSTANCIA -->
<script>
module.exports = {
  data: function () {
    return {
      greeting: 'Hello'
    }
  }
}
</script>

<!-- ESTILOS -->
<style lang="stylus" scoped>
p
  font-size: 2rem;
  text-align: center;
</style>