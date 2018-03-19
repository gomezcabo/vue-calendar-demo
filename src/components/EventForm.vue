<template>
  <div>
    <h1>Nuevo Evento</h1>

    <!-- TWO WAY DATA BINDING -->
    <input
      type="text"
      placeholder="Descripción del evento..."
      v-model="eventDescription"
      @keyup.enter="add"
    />

    <!-- EVENT BINDING -->
    <button @click="add">Añadir</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      eventDescription: ''
    }
  },
  methods: {
    add () {
      if (this.eventDescription.trim().length > 0) {
        this.$emit('eventCreated', this.eventDescription)
        this.eventDescription = ''
      }
    }
  }
}
</script>

<style lang="scss" scoped>
div {
  // display: flex;
  // flex-direction: column;
}

input, button {
  box-sizing: border-box;
  padding: 4px 10px;
  height: 32px;
}
</style>

