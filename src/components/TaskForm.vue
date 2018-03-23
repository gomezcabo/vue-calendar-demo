<template>
  <div>
    <h1>Nueva Tarea</h1>

    <!-- TWO WAY DATA BINDING -->
    <input
      type="text"
      placeholder="Descripción de la tarea..."
      v-model="taskDescription"
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
      taskDescription: ''
    }
  },
  methods: {
    add () {
      if (this.taskDescription.trim().length > 0) {
        this.$emit('taskCreated', this.taskDescription)
        this.taskDescription = ''
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
