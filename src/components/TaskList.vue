<template>
  <div id="task-list">
    <h1>Tareas</h1>

    <!-- CONDITIONAL RENDERING -->
    <div class="empty" v-if="tasks.length === 0">
      No hay tareas para este día
    </div>
    <template v-else>
      <div class="task" v-for="task of tasks" :key="task.id">
        <div class="description">
          {{ task.description }}
        </div>
        <div class="delete" @click="$emit('deletedTask', task.id)">
          Eliminar
        </div>
      </div>
    </template>

  </div>
</template>

<script>
export default {
  props: {
    tasks: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style lang="scss" scoped>
#task-list {
  .task {
    padding: 15px 20px;
    border: 1px solid #ddd;
    margin: 8px 0;
    display: flex;
    justify-content: space-between;

    .delete {
      cursor: pointer;
      color: darkred;
      font-weight: bold;
    }
  }

  .empty {
    padding-top: 20px;
  }
}

h1 {
  margin: -4px 0 34px 0;
}
</style>
