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
    <button @click="add">AÑADIR</button>
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

input, button {
  box-sizing: border-box;
  padding: 4px 10px;
  height: 32px;
  border: 1px solid #777
}

button {
  width: 100px;
  color: white;
  background: #de3800;
  border: 1px solid transparent;
  font-weight: bold;
  cursor: pointer;

  &:focus {
    outline: 0;
  }
}

input {
  width: calc(100% - 110px);
}
</style>
